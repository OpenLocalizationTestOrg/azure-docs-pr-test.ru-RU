---
title: "Создание кластеров Hadoop с помощью шаблонов Azure HDInsight | Документация Майкрософт"
description: "Узнайте о создании кластеров для HDInsight с помощью шаблонов Resource Manager."
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
ms.openlocfilehash: b2cdc954530daea2a641599c946ce3787149e762
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="38652-103">Создание кластеров Hadoop в HDInsight с помощью шаблонов Resource Manager</span><span class="sxs-lookup"><span data-stu-id="38652-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="38652-104">В этой статье вы изучите несколько способов создания кластеров Azure HDInsight с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="38652-104">In this article, you learn several ways to create Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="38652-105">Узнайте подробнее [о развертывании приложения с помощью шаблона диспетчера ресурсов Azure](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="38652-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="38652-106">Сведения о других инструментах и функциях создания кластеров можно получить, воспользовавшись селектором вкладок в верхней части этой страницы или ознакомившись с разделом [Способы создания кластера](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span><span class="sxs-lookup"><span data-stu-id="38652-106">To learn about other cluster creation tools and features, click the tab selector on the top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38652-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="38652-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="38652-108">Для выполнения инструкций этой статье понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="38652-108">To follow the instructions in this article, you'll need:</span></span>

* <span data-ttu-id="38652-109"><seg>
  [Подписка Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</seg></span><span class="sxs-lookup"><span data-stu-id="38652-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="38652-110">Azure PowerShell и (или) Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="38652-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="38652-111">Шаблоны диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="38652-111">Resource Manager templates</span></span>
<span data-ttu-id="38652-112">Шаблон Resource Manager упрощает создание для приложения приведенных ниже компонентов с помощью отдельной скоординированной операции:</span><span class="sxs-lookup"><span data-stu-id="38652-112">A Resource Manager template makes it easy to create the following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="38652-113">кластеры HDInsight и зависимые ресурсы (например, учетная запись хранения по умолчанию);</span><span class="sxs-lookup"><span data-stu-id="38652-113">HDInsight clusters and their dependent resources (such as the default storage account)</span></span>
* <span data-ttu-id="38652-114">другие ресурсы (например, база данных SQL Azure для использования Apache Sqoop).</span><span class="sxs-lookup"><span data-stu-id="38652-114">Other resources (such as Azure SQL Database to use Apache Sqoop)</span></span>

<span data-ttu-id="38652-115">В шаблоне определяются ресурсы, необходимые для приложения.</span><span class="sxs-lookup"><span data-stu-id="38652-115">In the template, you define the resources that are needed for the application.</span></span> <span data-ttu-id="38652-116">Можно также указать параметры развертывания в качестве входных значений для различных сред.</span><span class="sxs-lookup"><span data-stu-id="38652-116">You also specify deployment parameters to input values for different environments.</span></span> <span data-ttu-id="38652-117">Шаблон состоит из кода JSON и выражений, на основе которых можно создавать значения для развертывания.</span><span class="sxs-lookup"><span data-stu-id="38652-117">The template consists of JSON and expressions that you use to construct values for your deployment.</span></span>

<span data-ttu-id="38652-118">Примеры шаблонов HDInsight можно найти в [коллекции шаблонов быстрого запуска Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="38652-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="38652-119">Используйте кроссплатформенный редактор [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) с [расширением Resource Manager](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) или текстовый редактор, чтобы сохранить шаблон в файл на своей рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="38652-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with the [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor to save the template into a file on your workstation.</span></span> <span data-ttu-id="38652-120">Далее вы узнаете, как вызвать шаблон разными способами.</span><span class="sxs-lookup"><span data-stu-id="38652-120">You learn how to call the template by using different methods.</span></span>

<span data-ttu-id="38652-121">Дополнительные сведения о шаблонах Resource Manager см. в перечисленных ниже статьях.</span><span class="sxs-lookup"><span data-stu-id="38652-121">For more information about Resource Manager templates, see the following articles:</span></span>

* [<span data-ttu-id="38652-122">Шаблоны диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="38652-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="38652-123">Развертывание ресурсов с использованием шаблонов Resource Manager и Azure CLI</span><span class="sxs-lookup"><span data-stu-id="38652-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="38652-124">Создание шаблонов</span><span class="sxs-lookup"><span data-stu-id="38652-124">Generate templates</span></span>

<span data-ttu-id="38652-125">С помощью портала Azure можно настроить все параметры кластера и сохранить шаблон перед его развертыванием.</span><span class="sxs-lookup"><span data-stu-id="38652-125">By using the Azure portal, you can configure all the properties of a cluster and then save the template before deploying it.</span></span> <span data-ttu-id="38652-126">Затем можно будет многократно использовать этот шаблон.</span><span class="sxs-lookup"><span data-stu-id="38652-126">You can then reuse the template.</span></span>

<span data-ttu-id="38652-127">**Создание шаблона с помощью портала Azure**</span><span class="sxs-lookup"><span data-stu-id="38652-127">**To generate a template by using the Azure portal**</span></span>

1. <span data-ttu-id="38652-128">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="38652-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="38652-129">Щелкните **Создать** в меню слева, выберите **Аналитика** и щелкните **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="38652-129">Click **New** on the left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="38652-130">Следуя инструкциям, укажите свойства.</span><span class="sxs-lookup"><span data-stu-id="38652-130">Follow the instructions to enter properties.</span></span> <span data-ttu-id="38652-131">Можно использовать параметр **Быстрое создание** или **Настраиваемый**.</span><span class="sxs-lookup"><span data-stu-id="38652-131">You can use either the **Quick create** or the **Custom** option.</span></span>
4. <span data-ttu-id="38652-132">На вкладке **Сводка** щелкните **Скачать шаблон и параметры**.</span><span class="sxs-lookup"><span data-stu-id="38652-132">On the **Summary** tab, click **Download template and parameters**:</span></span>

    ![Скачивание шаблона Resource Manager для создания кластера HDInsight Hadoop](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="38652-134">Будут отображены файл шаблона, файл параметров и примеры кода для развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="38652-134">You see a list of the template file, parameters file, and code samples used to deploy the template:</span></span>

    ![Параметры скачивания шаблона Resource Manager для создания кластера HDInsight Hadoop](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="38652-136">Отсюда шаблон можно скачать, сохранить его в библиотеке шаблонов или развернуть.</span><span class="sxs-lookup"><span data-stu-id="38652-136">From here, you can download the template, save it to your template library, or deploy the template.</span></span>

    <span data-ttu-id="38652-137">Чтобы использовать шаблон из библиотеки, щелкните **Больше служб** в меню слева, а затем щелкните **Шаблоны** (в категории **Другое**).</span><span class="sxs-lookup"><span data-stu-id="38652-137">To access a template in your library, click **More services** from the left menu, and then click **Templates** (under the **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="38652-138">Файл шаблона и файл параметров должны использоваться вместе.</span><span class="sxs-lookup"><span data-stu-id="38652-138">The template and parameters file must be used together.</span></span> <span data-ttu-id="38652-139">В противном случае можно получить непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="38652-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="38652-140">Например, значением свойства **clusterKind** по умолчанию всегда будет **hadoop**, несмотря на то, что вы указали перед скачиванием файла шаблона.</span><span class="sxs-lookup"><span data-stu-id="38652-140">For example, the default **clusterKind** property value is always **hadoop**, despite what you specify before you download the template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="38652-141">Развертывание с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="38652-141">Deploy with PowerShell</span></span>

<span data-ttu-id="38652-142">В этой процедуре создается кластер Hadoop в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38652-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="38652-143">Сохраните JSON-файл из [приложения](#appx-a-arm-template) на своей рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="38652-143">Save the JSON file in the [Appendix](#appx-a-arm-template) to your workstation.</span></span> <span data-ttu-id="38652-144">В сценарии PowerShell имя файла — `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="38652-144">In the PowerShell script, the file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="38652-145">При необходимости настройте параметры и переменные.</span><span class="sxs-lookup"><span data-stu-id="38652-145">Set the parameters and variables if needed.</span></span>
3. <span data-ttu-id="38652-146">Запустите шаблон с помощью следующего сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38652-146">Run the template by using the following PowerShell script:</span></span>

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
        # Connect to Azure
        ####################################
        #region - Connect to Azure subscription
        Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and the dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="38652-147">Сценарий PowerShell настраивает только имя кластера.</span><span class="sxs-lookup"><span data-stu-id="38652-147">The PowerShell script configures only the cluster name.</span></span> <span data-ttu-id="38652-148">Имя учетной записи хранения жестко запрограммировано в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="38652-148">The storage account name is hard-coded in the template.</span></span> <span data-ttu-id="38652-149">Вам будет предложено ввести пароль пользователя кластера.</span><span class="sxs-lookup"><span data-stu-id="38652-149">You are prompted to enter the cluster user password.</span></span> <span data-ttu-id="38652-150">Имя пользователя по умолчанию — **admin**. Вам также будет предложено ввести пароль пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="38652-150">(The default username is **admin**.) You are also prompted to enter the SSH user password.</span></span> <span data-ttu-id="38652-151">Имя пользователя SSH по умолчанию — **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="38652-151">(The default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="38652-152">Дополнительные сведения см. в статье [Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="38652-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="38652-153">Развертывание с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="38652-153">Deploy with CLI</span></span>
<span data-ttu-id="38652-154">В следующем примере используется интерфейс командной строки Azure (CLI).</span><span class="sxs-lookup"><span data-stu-id="38652-154">The following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="38652-155">Он создает кластер и его учетную запись хранения и контейнер, вызывая шаблон Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="38652-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="38652-156">Вам будет предложено ввести следующие значения.</span><span class="sxs-lookup"><span data-stu-id="38652-156">You are prompted to enter:</span></span>
* <span data-ttu-id="38652-157">Имя кластера.</span><span class="sxs-lookup"><span data-stu-id="38652-157">The cluster name.</span></span>
* <span data-ttu-id="38652-158">Пароль пользователя кластера.</span><span class="sxs-lookup"><span data-stu-id="38652-158">The cluster user password.</span></span> <span data-ttu-id="38652-159">Имя пользователя по умолчанию — **admin**.</span><span class="sxs-lookup"><span data-stu-id="38652-159">(The default username is **admin**.)</span></span>
* <span data-ttu-id="38652-160">Пароль пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="38652-160">The SSH user password.</span></span> <span data-ttu-id="38652-161">Имя пользователя SSH по умолчанию — **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="38652-161">(The default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="38652-162">В следующем коде содержатся встроенные параметры.</span><span class="sxs-lookup"><span data-stu-id="38652-162">The following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="38652-163">Развертывание с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="38652-163">Deploy with the REST API</span></span>
<span data-ttu-id="38652-164">См. статью [Развертывание ресурсов с использованием шаблонов и REST API Resource Manager](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="38652-164">See [Deploy with the REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="38652-165">Развертывание с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="38652-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="38652-166">С помощью Visual Studio можно создать проект группы ресурсов и развернуть его в Azure, используя пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="38652-166">Use Visual Studio to create a resource group project and deploy it to Azure through the user interface.</span></span> <span data-ttu-id="38652-167">Выберите тип ресурсов, добавляемых в проект.</span><span class="sxs-lookup"><span data-stu-id="38652-167">You select the type of resources to include in your project.</span></span> <span data-ttu-id="38652-168">Эти ресурсы автоматически добавляются в шаблон Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="38652-168">Those resources are automatically added to the Resource Manager template.</span></span> <span data-ttu-id="38652-169">Проект также предоставляет сценарий PowerShell для развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="38652-169">The project also provides a PowerShell script to deploy the template.</span></span>

<span data-ttu-id="38652-170">Обзорные сведения об использовании групп ресурсов в Visual Studio см. в статье [Создание и развертывание групп ресурсов Azure с помощью Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="38652-170">For an introduction to using Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="38652-171">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="38652-171">Troubleshoot</span></span>

<span data-ttu-id="38652-172">Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="38652-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="38652-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="38652-173">Next steps</span></span>
<span data-ttu-id="38652-174">В этой статье вы ознакомились с несколькими способами создания кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38652-174">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="38652-175">Для получения дополнительных сведений ознакомьтесь со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="38652-175">To learn more, see the following articles:</span></span>

* <span data-ttu-id="38652-176">Пример развертывания ресурсов с помощью клиентской библиотеки .NET см. в статье [Развертывание виртуальной машины Azure с помощью C# и шаблона Resource Manager](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="38652-176">For an example of deploying resources through the .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="38652-177">Подробный пример развертывания приложения см. в статье [Предсказуемые подготовка и развертывание микрослужб в Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="38652-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="38652-178">Инструкции по развертыванию своего решения в различных средах см. в статье [Среды разработки и тестирования в Microsoft Azure](../solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="38652-178">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="38652-179">Дополнительную информацию о разделах в шаблоне Azure Resource Manager см. в статье [Создание шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="38652-179">To learn about the sections of the Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="38652-180">Список функций, которые можно использовать в шаблоне Azure Resource Manager, см. в статье [Функции шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="38652-180">For a list of the functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-to-create-a-hadoop-cluster"></a><span data-ttu-id="38652-181">Приложение. Использование шаблона Resource Manager для создания кластера Hadoop</span><span class="sxs-lookup"><span data-stu-id="38652-181">Appendix: Resource Manager template to create a Hadoop cluster</span></span>
<span data-ttu-id="38652-182">Следующий шаблон Azure Resource Manager создает кластер Hadoop под управлением Linux с зависимой учетной записью хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="38652-182">The following Azure Resource Manager template creates a Linux-based Hadoop cluster with the dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="38652-183">В этом примере содержатся сведения о конфигурации для хранилищ метаданных Hive и Oozie.</span><span class="sxs-lookup"><span data-stu-id="38652-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="38652-184">Удалите раздел или настройте его перед использованием шаблона.</span><span class="sxs-lookup"><span data-stu-id="38652-184">Remove the section or configure the section before using the template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "The name of the HDInsight cluster to create."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used to remotely access the cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
            "description": "The location where all azure resources will be deployed."
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
            "description": "The type of the HDInsight cluster to create."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "The number of nodes in the HDInsight cluster."
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

## <a name="appendix-resource-manager-template-to-create-a-spark-cluster"></a><span data-ttu-id="38652-185">Приложение. Использование шаблона Resource Manager для создания кластера Spark</span><span class="sxs-lookup"><span data-stu-id="38652-185">Appendix: Resource Manager template to create a Spark cluster</span></span>

<span data-ttu-id="38652-186">В этом разделе содержатся сведения Resource Manager для создания кластера HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="38652-186">This section provides a Resource Manager template that you can use to create an HDInsight Spark cluster.</span></span> <span data-ttu-id="38652-187">Этот шаблон содержит настройки для `spark-defaults` и `spark-thrift-sparkconf` (для кластеров Spark 1.6), а также для `spark2-defaults` и `spark2-thrift-sparkconf` (для кластеров Spark 2).</span><span class="sxs-lookup"><span data-stu-id="38652-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="38652-188">Кроме того, HDInsight вычисляет и задает конфигурации, такие как `spark.executor.instances`, `spark.executor.memory` и `spark.executor.cores`, на основе размера кластера.</span><span class="sxs-lookup"><span data-stu-id="38652-188">In addition to this, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on the cluster size.</span></span> 

<span data-ttu-id="38652-189">Если задать любой из параметров этого раздела как часть самого шаблона, HDInsight не будет рассчитывать и задавать другие параметры того же раздела.</span><span class="sxs-lookup"><span data-stu-id="38652-189">If you set any one parameter in a section as part of the template itself, HDInsight does not calculate and set the other parameters of the same section.</span></span> <span data-ttu-id="38652-190">Например, параметр `spark.executor.instances` относится к конфигурации `spark-defaults`.</span><span class="sxs-lookup"><span data-stu-id="38652-190">For example, parameter `spark.executor.instances` is in the  `spark-defaults` configuration.</span></span> <span data-ttu-id="38652-191">Если задать другой параметр (например, `spark.yarn.exector.memoryOverhead`) в конфигурации `spark-defaults`, HDInsight также не будет рассчитывать и задавать параметр `spark.executor.instances`.</span><span class="sxs-lookup"><span data-stu-id="38652-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in the `spark-defaults` configuration, HDInsight does not calculate and set the `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "The name of the HDInsight cluster to create."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "The location where all azure resources will be deployed."
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
                "description": "The number of nodes in the HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "The type of the HDInsight cluster to create."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used to remotely access the cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
