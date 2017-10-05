---
title: "Создание кластеров HBase в виртуальной сети Azure | Документация Майкрософт"
description: "Приступите к работе с HBase в Azure HDInsight. Узнайте, как создать кластеры HDInsight HBase в виртуальной сети Azure."
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 668bd494ce3274188af56cf7d6253cec7af9abbc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="4238a-104">Создание кластеров HBase в HDInsight в виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="4238a-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="4238a-105">Узнайте, как создавать кластеры Azure HDInsight HBase в [виртуальной сети Azure][1].</span><span class="sxs-lookup"><span data-stu-id="4238a-105">Learn how to create Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="4238a-106">Благодаря интеграции виртуальной сети кластеры HBase могут быть развернуты в той же виртуальной сети, что и приложения. Это позволяет приложениям взаимодействовать с HBase непосредственно.</span><span class="sxs-lookup"><span data-stu-id="4238a-106">With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="4238a-107">К преимуществам относятся:</span><span class="sxs-lookup"><span data-stu-id="4238a-107">The benefits include:</span></span>

* <span data-ttu-id="4238a-108">прямое подключение веб-приложения к узлам кластера HBase, который обеспечивает обмен данными с помощью интерфейсов API удаленного вызова процедур (RPC) Java для HBase;</span><span class="sxs-lookup"><span data-stu-id="4238a-108">Direct connectivity of the web application to the nodes of the HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="4238a-109">повышение производительности без необходимости организации пропуска трафика через множество шлюзов и подсистемы балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="4238a-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="4238a-110">возможность обработки конфиденциальной информации более безопасным способом, без необходимости организации общедоступной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="4238a-110">The ability to process sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4238a-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4238a-111">Prerequisites</span></span>
<span data-ttu-id="4238a-112">Перед началом работы с этим руководством необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="4238a-112">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="4238a-113">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="4238a-113">**An Azure subscription**.</span></span> <span data-ttu-id="4238a-114">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="4238a-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="4238a-115"><seg>
  **Рабочая станция с Azure PowerShell**.</seg></span><span class="sxs-lookup"><span data-stu-id="4238a-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="4238a-116">Обратитесь к разделу [Установка и использование Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span><span class="sxs-lookup"><span data-stu-id="4238a-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="4238a-117">Создание кластера HBase в виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="4238a-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="4238a-118">В этом разделе мы создадим кластер HBase под управлением Linux с зависимой учетной записью службы хранилища Azure в виртуальной сети Azure c помощью [шаблона Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="4238a-118">In this section, you create a Linux-based HBase cluster with the dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="4238a-119">Сведения о других способах создания кластеров и их параметрах см. в статье [Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="4238a-119">For other cluster creation methods and understanding the settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="4238a-120">Дополнительные сведения о создании в HDInsight кластеров Hadoop с помощью шаблонов ARM см. в статье [Создание кластеров Hadoop под управлением Windows в HDInsight с помощью шаблонов Azure Resource Manager](hdinsight-hadoop-create-windows-clusters-arm-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4238a-120">For more information about using a template to create Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="4238a-121">Некоторые свойства жестко заданы в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="4238a-121">Some properties are hard-coded into the template.</span></span> <span data-ttu-id="4238a-122">Например:</span><span class="sxs-lookup"><span data-stu-id="4238a-122">For example:</span></span>
>
> * <span data-ttu-id="4238a-123">**Расположение**: восточный регион США 2.</span><span class="sxs-lookup"><span data-stu-id="4238a-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="4238a-124">**Версия кластера**: 3.5.</span><span class="sxs-lookup"><span data-stu-id="4238a-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="4238a-125">**Число рабочих узлов кластера**: 2.</span><span class="sxs-lookup"><span data-stu-id="4238a-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="4238a-126">**Учетная запись хранения по умолчанию**: уникальная строка</span><span class="sxs-lookup"><span data-stu-id="4238a-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="4238a-127">**Имя виртуальной сети**: &lt;имя_кластера>-vnet.</span><span class="sxs-lookup"><span data-stu-id="4238a-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="4238a-128">**Адресное пространство виртуальной сети**: 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="4238a-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="4238a-129">**Имя подсети**: subnet1</span><span class="sxs-lookup"><span data-stu-id="4238a-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="4238a-130">**Диапазон адресов подсети**: 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="4238a-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="4238a-131">Заполнитель &lt;имя_кластера> будет заменен именем кластера, которое вы укажете при использовании шаблона.</span><span class="sxs-lookup"><span data-stu-id="4238a-131">&lt;Cluster Name> is replaced with the cluster name you provide when using the template.</span></span>
>
>

1. <span data-ttu-id="4238a-132">Щелкните следующее изображение, чтобы открыть шаблон на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="4238a-132">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="4238a-133">Шаблон находится в [шаблонах быстрого запуска Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span><span class="sxs-lookup"><span data-stu-id="4238a-133">The template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="4238a-134">В колонке **Настраиваемое развертывание** укажите следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="4238a-134">From the **Custom deployment** blade, enter the following properties:</span></span>

   * <span data-ttu-id="4238a-135">**Подписка**. Выберите подписку Azure, которая использовалась для создания кластера HDInsight, зависимой учетной записи хранения и виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="4238a-135">**Subscription**: Select an Azure subscription used to create the HDInsight cluster, the dependent Storage account and the Azure virtual network.</span></span>
   * <span data-ttu-id="4238a-136">**Группа ресурсов**.Щелкните **Создать** и укажите имя новой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4238a-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="4238a-137">**Расположение**. Выберите расположение группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4238a-137">**Location**: Select a location for the resource group.</span></span>
   * <span data-ttu-id="4238a-138">**Имя_кластера**. Введите имя создаваемого кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="4238a-138">**ClusterName**: Enter a name for the Hadoop cluster to be created.</span></span>
   * <span data-ttu-id="4238a-139">**Имя для входа и пароль кластера**: имя для входа по умолчанию — **admin**.</span><span class="sxs-lookup"><span data-stu-id="4238a-139">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="4238a-140">**Имя пользователя SSH и пароль**: по умолчанию используется имя **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="4238a-140">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="4238a-141">Это имя можно изменить.</span><span class="sxs-lookup"><span data-stu-id="4238a-141">You can rename it.</span></span>
   * <span data-ttu-id="4238a-142">**Я принимаю указанные выше условия**. Установите этот флажок.</span><span class="sxs-lookup"><span data-stu-id="4238a-142">**I agree to the terms and the conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="4238a-143">Щелкните **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="4238a-143">Click **Purchase**.</span></span> <span data-ttu-id="4238a-144">Процесс создания кластера занимает около 20 минут.</span><span class="sxs-lookup"><span data-stu-id="4238a-144">It takes about around 20 minutes to create a cluster.</span></span> <span data-ttu-id="4238a-145">Когда кластер будет создан, щелкните его колонку на портале, чтобы открыть его.</span><span class="sxs-lookup"><span data-stu-id="4238a-145">Once the cluster is created, you can click the cluster blade in the portal to open it.</span></span>

<span data-ttu-id="4238a-146">После завершения работы с этим руководством кластер можно удалить.</span><span class="sxs-lookup"><span data-stu-id="4238a-146">After you complete the tutorial, you might want to delete the cluster.</span></span> <span data-ttu-id="4238a-147">В случае с HDInsight ваши данные хранятся в службе хранилища Azure, что позволяет безопасно удалить неиспользуемый кластер.</span><span class="sxs-lookup"><span data-stu-id="4238a-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="4238a-148">Плата за кластеры HDInsight взимается, даже когда они не используются.</span><span class="sxs-lookup"><span data-stu-id="4238a-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="4238a-149">Поскольку стоимость кластера во много раз превышает стоимость хранилища, экономически целесообразно удалять неиспользуемые кластеры.</span><span class="sxs-lookup"><span data-stu-id="4238a-149">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span> <span data-ttu-id="4238a-150">Инструкции по удалению кластера см. в статье [Управление кластерами Hadoop в HDInsight с помощью портала Azure](hdinsight-administer-use-management-portal.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="4238a-150">For the instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using the Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="4238a-151">Чтобы начать работу с новым HBase кластером, можно использовать процедуры, которые представлены в разделе [Приступая к работе с HBase с Hadoop в HDInsight](hdinsight-hbase-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4238a-151">To begin working with your new HBase cluster, you can use the procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-to-the-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="4238a-152">Подключитесь к кластеру HBase с помощью API-интерфейсов удаленного вызова процедур Java HBase</span><span class="sxs-lookup"><span data-stu-id="4238a-152">Connect to the HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="4238a-153">Создайте виртуальную машину IaaS в той же виртуальной сети Azure и той же подсети.</span><span class="sxs-lookup"><span data-stu-id="4238a-153">Create an infrastructure as a service (IaaS) virtual machine into the same Azure virtual network and the same subnet.</span></span> <span data-ttu-id="4238a-154">Инструкции по созданию виртуальной машины IaaS см. в статье [Создание первой виртуальной машины Windows на портале Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="4238a-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="4238a-155">При выполнении действий, описанных в этом документе, необходимо использовать следующие значения для конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="4238a-155">When following the steps in this document, you must use the following values for the Network configuration:</span></span>

   * <span data-ttu-id="4238a-156">**Виртуальная сеть**: &lt;имя_кластера>-vnet.</span><span class="sxs-lookup"><span data-stu-id="4238a-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="4238a-157">**Подсеть**: subnet1</span><span class="sxs-lookup"><span data-stu-id="4238a-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4238a-158">Замените &lt;имя_кластера> именем, использованным при создании кластера HDInsight на предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="4238a-158">Replace &lt;Cluster name> with the name you used when creating the HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="4238a-159">Благодаря этим значениям виртуальная машина будет размещена в той же виртуальной сети и подсети, что и кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4238a-159">Using these values, the virtual machine is placed in the same virtual network and subnet as the HDInsight cluster.</span></span> <span data-ttu-id="4238a-160">Эта конфигурация позволит им напрямую взаимодействовать друг с другом.</span><span class="sxs-lookup"><span data-stu-id="4238a-160">This configuration allows them to directly communicate with each other.</span></span> <span data-ttu-id="4238a-161">Существует возможность создания кластера HDInsight с пустым граничным узлом.</span><span class="sxs-lookup"><span data-stu-id="4238a-161">There is a way to create an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="4238a-162">Граничный узел можно использовать для управления кластером.</span><span class="sxs-lookup"><span data-stu-id="4238a-162">The edge node can be used to manage the cluster.</span></span>  <span data-ttu-id="4238a-163">Подробные сведения см. в статье [Использование пустых граничных узлов в HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="4238a-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="4238a-164">При использовании Java-приложения для удаленного подключения к HBase необходимо использовать полное доменное имя (FQDN).</span><span class="sxs-lookup"><span data-stu-id="4238a-164">When using a Java application to connect to HBase remotely, you must use the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="4238a-165">Чтобы определить это, вам необходимо получить DNS-суффикс кластера HBase.</span><span class="sxs-lookup"><span data-stu-id="4238a-165">To determine this, you must get the connection-specific DNS suffix of the HBase cluster.</span></span> <span data-ttu-id="4238a-166">Для этого используйте один из следующих методов.</span><span class="sxs-lookup"><span data-stu-id="4238a-166">To do that, you can use one of the following methods:</span></span>

   * <span data-ttu-id="4238a-167">С помощью веб-браузера сделайте вызов Ambari.</span><span class="sxs-lookup"><span data-stu-id="4238a-167">Use a Web browser to make an Ambari call:</span></span>

     <span data-ttu-id="4238a-168">Перейдите по адресу: https://&lt;имя_кластера>.azurehdinsight.net/api/v1/clusters/&lt;имя_кластера>/hosts?minimal_response=true.</span><span class="sxs-lookup"><span data-stu-id="4238a-168">Browse to https://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="4238a-169">Он вернет файл JSON с DNS-суффиксами.</span><span class="sxs-lookup"><span data-stu-id="4238a-169">It turns a JSON file with the DNS suffixes.</span></span>
   * <span data-ttu-id="4238a-170">Используйте веб-сайт Ambari.</span><span class="sxs-lookup"><span data-stu-id="4238a-170">Use the Ambari website:</span></span>

     1. <span data-ttu-id="4238a-171">Перейдите по адресу: https://&lt;имя_кластера>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="4238a-171">Browse to  https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="4238a-172">В верхнем меню щелкните **Hosts** (Узлы).</span><span class="sxs-lookup"><span data-stu-id="4238a-172">Click **Hosts** from the top menu.</span></span>
   * <span data-ttu-id="4238a-173">Используйте Curl, чтобы выполнить вызовы REST:</span><span class="sxs-lookup"><span data-stu-id="4238a-173">Use Curl to make REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="4238a-174">В возвращенных данных JSON найдите запись «host_name».</span><span class="sxs-lookup"><span data-stu-id="4238a-174">In the JavaScript Object Notation (JSON) data returned, find the "host_name" entry.</span></span> <span data-ttu-id="4238a-175">Она содержит полные доменные имена узлов в кластере.</span><span class="sxs-lookup"><span data-stu-id="4238a-175">It contains the FQDN for the nodes in the cluster.</span></span> <span data-ttu-id="4238a-176">Например:</span><span class="sxs-lookup"><span data-stu-id="4238a-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="4238a-177">Часть доменного имени, начинающаяся с имени кластера, является DNS-суффиксом.</span><span class="sxs-lookup"><span data-stu-id="4238a-177">The portion of the domain name beginning with the cluster name is the DNS suffix.</span></span> <span data-ttu-id="4238a-178">Например, mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="4238a-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="4238a-179">Использование Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4238a-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="4238a-180">Используйте следующий скрипт Azure PowerShell для регистрации функции **Get-ClusterDetail** , которую можно использовать для возвращения DNS-суффикса.</span><span class="sxs-lookup"><span data-stu-id="4238a-180">Use the following Azure PowerShell script to register the **Get-ClusterDetail** function, which can be used to return the DNS suffix:</span></span>

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information to facilitate an HDInsight cluster-to-cluster scenario within the same virtual network.
            .Description
            This command shows the following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows the value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows the value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run the HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows the FQDN suffix of hosts in the cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows the value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows the value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run the HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows the FQDN suffix of hosts in the cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     <span data-ttu-id="4238a-181">После запуска сценария Azure PowerShell используйте следующую команду, чтобы вернуть DNS-суффикс с помощью функции **Get-ClusterDetail** .</span><span class="sxs-lookup"><span data-stu-id="4238a-181">After running the Azure PowerShell script, use the following command to return the DNS suffix by using the **Get-ClusterDetail** function.</span></span> <span data-ttu-id="4238a-182">При использовании этой команды укажите имя кластера HDInsight HBase, имя и пароль администратора.</span><span class="sxs-lookup"><span data-stu-id="4238a-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="4238a-183">Эта команда возвращает DNS-суффикс.</span><span class="sxs-lookup"><span data-stu-id="4238a-183">This command returns the DNS suffix.</span></span> <span data-ttu-id="4238a-184">Например, **yourclustername.b4.internal.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="4238a-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change the primary DNS suffix configuration of the virtual machine. This enables the virtual machine to automatically resolve the host name of the HBase cluster without explicit specification of the suffix. For example, the *workernode0* host name will be correctly resolved to workernode0 of the HBase cluster.

    To make the configuration change:

    1. RDP into the virtual machine.
    2. Open **Local Group Policy Editor**. The executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** to the value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot the virtual machine.
-->

<span data-ttu-id="4238a-185">Чтобы проверить обмен данными между виртуальной машиной и кластером HBase, используйте следующую команду `ping headnode0.<dns suffix>` на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="4238a-185">To verify that the virtual machine can communicate with the HBase cluster, use the command `ping headnode0.<dns suffix>` from the virtual machine.</span></span> <span data-ttu-id="4238a-186">Например, ping headnode0.mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="4238a-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="4238a-187">Чтобы использовать эту информацию в Java-приложении, для создания приложения можно придерживаться шагов, представленных в разделе [Использование Maven для создания Java-приложений, использующих HBase с HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) .</span><span class="sxs-lookup"><span data-stu-id="4238a-187">To use this information in a Java application, you can follow the steps in [Use Maven to build Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) to create an application.</span></span> <span data-ttu-id="4238a-188">Чтобы приложение подключилось к удаленному серверу HBase, измените файл **hbase-site.xml** в этом примере, чтобы использовать полное доменное имя для ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="4238a-188">To have the application connect to a remote HBase server, modify the **hbase-site.xml** file in this example to use the FQDN for Zookeeper.</span></span> <span data-ttu-id="4238a-189">Например:</span><span class="sxs-lookup"><span data-stu-id="4238a-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="4238a-190">Чтобы получить дополнительную информацию о разрешении имен в виртуальных сетях Azure, а также об использовании своего​ собственного DNS-сервера, ознакомьтесь со статьей [Разрешение имен для ВМ и экземпляров ролей](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="4238a-190">For more information about name resolution in Azure virtual networks, including how to use your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="4238a-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4238a-191">Next steps</span></span>
<span data-ttu-id="4238a-192">Из этого руководства вы узнали, как создать кластер HBase.</span><span class="sxs-lookup"><span data-stu-id="4238a-192">In this tutorial, you learned how to create an HBase cluster.</span></span> <span data-ttu-id="4238a-193">Дополнительные сведения см. на следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="4238a-193">To learn more, see:</span></span>

* [<span data-ttu-id="4238a-194">Приступая к работе с HDInsight</span><span class="sxs-lookup"><span data-stu-id="4238a-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="4238a-195">Использование пустых граничных узлов в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4238a-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="4238a-196">Настройка репликации HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4238a-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="4238a-197">Создание кластеров Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4238a-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="4238a-198">Приступая к работе с HBase с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4238a-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="4238a-199">Анализ мнений пользователей Twitter с использованием HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4238a-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="4238a-200">[Обзор виртуальной сети][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="4238a-200">[Virtual Network Overview][vnet-overview]</span></span>

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Подготовка сведений для нового кластера HBase"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Использование действия сценария для настройки кластера HBase"

[azure-preview-portal]: https://portal.azure.com
