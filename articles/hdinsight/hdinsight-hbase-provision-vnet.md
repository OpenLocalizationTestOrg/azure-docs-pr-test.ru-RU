---
title: "aaaCreate HBase кластеров в виртуальной сети - Azure | Документы Microsoft"
description: "Приступите к работе с HBase в Azure HDInsight. Узнайте, как кластеров HDInsight HBase toocreate в виртуальной сети Azure."
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
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="b675b-104">Создание кластеров HBase в HDInsight в виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="b675b-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="b675b-105">Узнайте, как toocreate Azure HDInsight HBase кластеров в [виртуальной сети Azure][1].</span><span class="sxs-lookup"><span data-stu-id="b675b-105">Learn how toocreate Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="b675b-106">Благодаря интеграции виртуальной сети, HBase кластеров может быть развернутой toohello виртуальных сетевых как приложения таким образом, приложения могут взаимодействовать с HBase напрямую.</span><span class="sxs-lookup"><span data-stu-id="b675b-106">With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="b675b-107">Hello имеет следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b675b-107">hello benefits include:</span></span>

* <span data-ttu-id="b675b-108">Прямое подключение узлов toohello приложения hello web hello HBase кластера, который обеспечивает взаимодействие через HBase Java удаленной процедуры вызова API (RPC).</span><span class="sxs-lookup"><span data-stu-id="b675b-108">Direct connectivity of hello web application toohello nodes of hello HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="b675b-109">повышение производительности без необходимости организации пропуска трафика через множество шлюзов и подсистемы балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="b675b-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="b675b-110">Hello возможность tooprocess конфиденциальные сведения в более безопасном режиме без предоставления общедоступную конечную точку.</span><span class="sxs-lookup"><span data-stu-id="b675b-110">hello ability tooprocess sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b675b-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b675b-111">Prerequisites</span></span>
<span data-ttu-id="b675b-112">Прежде чем начать работу с учебником, необходимо иметь hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b675b-112">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="b675b-113">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="b675b-113">**An Azure subscription**.</span></span> <span data-ttu-id="b675b-114">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b675b-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b675b-115"><seg>
  **Рабочая станция с Azure PowerShell**.</seg></span><span class="sxs-lookup"><span data-stu-id="b675b-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="b675b-116">Обратитесь к разделу [Установка и использование Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span><span class="sxs-lookup"><span data-stu-id="b675b-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="b675b-117">Создание кластера HBase в виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="b675b-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="b675b-118">В этом разделе создать кластер HBase под управлением Linux с hello зависимых учетной записи хранилища Azure в виртуальной сети Azure с помощью [шаблона Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b675b-118">In this section, you create a Linux-based HBase cluster with hello dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="b675b-119">Для других методов создания кластера и см. в основные сведения о настройке hello, [HDInsight, создания кластеров](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b675b-119">For other cluster creation methods and understanding hello settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="b675b-120">Дополнительные сведения об использовании шаблона toocreate Hadoop кластеров в HDInsight, см. в разделе [кластеров создать Hadoop в HDInsight с помощью шаблонов диспетчера ресурсов Azure](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="b675b-120">For more information about using a template toocreate Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="b675b-121">Некоторые свойства жестко запрограммированы в шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="b675b-121">Some properties are hard-coded into hello template.</span></span> <span data-ttu-id="b675b-122">Например:</span><span class="sxs-lookup"><span data-stu-id="b675b-122">For example:</span></span>
>
> * <span data-ttu-id="b675b-123">**Расположение**: восточный регион США 2.</span><span class="sxs-lookup"><span data-stu-id="b675b-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="b675b-124">**Версия кластера**: 3.5.</span><span class="sxs-lookup"><span data-stu-id="b675b-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="b675b-125">**Число рабочих узлов кластера**: 2.</span><span class="sxs-lookup"><span data-stu-id="b675b-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="b675b-126">**Учетная запись хранения по умолчанию**: уникальная строка</span><span class="sxs-lookup"><span data-stu-id="b675b-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="b675b-127">**Имя виртуальной сети**: &lt;имя_кластера>-vnet.</span><span class="sxs-lookup"><span data-stu-id="b675b-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="b675b-128">**Адресное пространство виртуальной сети**: 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="b675b-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="b675b-129">**Имя подсети**: subnet1</span><span class="sxs-lookup"><span data-stu-id="b675b-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="b675b-130">**Диапазон адресов подсети**: 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="b675b-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="b675b-131">&lt;Имя кластера > заменяется именем кластера hello, указываемые при использовании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="b675b-131">&lt;Cluster Name> is replaced with hello cluster name you provide when using hello template.</span></span>
>
>

1. <span data-ttu-id="b675b-132">Щелкните hello следующий шаблон hello tooopen изображения в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b675b-132">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="b675b-133">Hello шаблон находится в [шаблоны быстрый запуск Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span><span class="sxs-lookup"><span data-stu-id="b675b-133">hello template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="b675b-134">Из hello **развертывания пользовательского** колонке введите hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="b675b-134">From hello **Custom deployment** blade, enter hello following properties:</span></span>

   * <span data-ttu-id="b675b-135">**Подписки**: выберите кластер HDInsight подписку Azure, используемую toocreate hello, hello зависимых учетной записи хранилища и hello виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="b675b-135">**Subscription**: Select an Azure subscription used toocreate hello HDInsight cluster, hello dependent Storage account and hello Azure virtual network.</span></span>
   * <span data-ttu-id="b675b-136">**Группа ресурсов**.Щелкните **Создать** и укажите имя новой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b675b-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="b675b-137">**Расположение**: выберите расположение для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="b675b-137">**Location**: Select a location for hello resource group.</span></span>
   * <span data-ttu-id="b675b-138">**Имя_кластера**: Введите имя для hello Hadoop кластера toobe создан.</span><span class="sxs-lookup"><span data-stu-id="b675b-138">**ClusterName**: Enter a name for hello Hadoop cluster toobe created.</span></span>
   * <span data-ttu-id="b675b-139">**Имя входа и пароль кластера**: имя для входа по умолчанию hello **администратора**.</span><span class="sxs-lookup"><span data-stu-id="b675b-139">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="b675b-140">**SSH имя пользователя и пароль**: имя пользователя по умолчанию hello **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="b675b-140">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="b675b-141">Это имя можно изменить.</span><span class="sxs-lookup"><span data-stu-id="b675b-141">You can rename it.</span></span>
   * <span data-ttu-id="b675b-142">**Я принимаю условия hello, указанных выше, toohello**: (флажок)</span><span class="sxs-lookup"><span data-stu-id="b675b-142">**I agree toohello terms and hello conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="b675b-143">Щелкните **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="b675b-143">Click **Purchase**.</span></span> <span data-ttu-id="b675b-144">Это занимает около toocreate около 20 минут кластера.</span><span class="sxs-lookup"><span data-stu-id="b675b-144">It takes about around 20 minutes toocreate a cluster.</span></span> <span data-ttu-id="b675b-145">После создания кластера hello hello кластера колонки в hello портала tooopen можно щелкнуть его.</span><span class="sxs-lookup"><span data-stu-id="b675b-145">Once hello cluster is created, you can click hello cluster blade in hello portal tooopen it.</span></span>

<span data-ttu-id="b675b-146">После завершения учебника hello, может потребоваться toodelete hello кластера.</span><span class="sxs-lookup"><span data-stu-id="b675b-146">After you complete hello tutorial, you might want toodelete hello cluster.</span></span> <span data-ttu-id="b675b-147">В случае с HDInsight ваши данные хранятся в службе хранилища Azure, что позволяет безопасно удалить неиспользуемый кластер.</span><span class="sxs-lookup"><span data-stu-id="b675b-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="b675b-148">Плата за кластеры HDInsight взимается, даже когда они не используются.</span><span class="sxs-lookup"><span data-stu-id="b675b-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="b675b-149">Поскольку плата hello для кластера hello много раз больше, чем hello плата за хранилище, экономически выгодно toodelete кластеры, когда они не используются.</span><span class="sxs-lookup"><span data-stu-id="b675b-149">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span> <span data-ttu-id="b675b-150">Hello инструкции удаления кластера см. в разделе [кластеров управление Hadoop в HDInsight с помощью hello портал Azure](hdinsight-administer-use-management-portal.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="b675b-150">For hello instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using hello Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="b675b-151">Работа с на новый кластер HBase toobegin можно использовать процедуры hello в [приступить к работе с базой HBase на Hadoop в HDInsight](hdinsight-hbase-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b675b-151">toobegin working with your new HBase cluster, you can use hello procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="b675b-152">Подключите кластер HBase toohello, с помощью API-интерфейсов RPC Java HBase</span><span class="sxs-lookup"><span data-stu-id="b675b-152">Connect toohello HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="b675b-153">Создавать инфраструктуру как услугу (IaaS) виртуальной машины в одной виртуальной сети Azure hello и hello одной подсети.</span><span class="sxs-lookup"><span data-stu-id="b675b-153">Create an infrastructure as a service (IaaS) virtual machine into hello same Azure virtual network and hello same subnet.</span></span> <span data-ttu-id="b675b-154">Инструкции по созданию виртуальной машины IaaS см. в статье [Создание первой виртуальной машины Windows на портале Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="b675b-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="b675b-155">При следующие hello в данном пошаговом руководстве, необходимо использовать следующие значения для конфигурации сети hello hello:</span><span class="sxs-lookup"><span data-stu-id="b675b-155">When following hello steps in this document, you must use hello following values for hello Network configuration:</span></span>

   * <span data-ttu-id="b675b-156">**Виртуальная сеть**: &lt;имя_кластера>-vnet.</span><span class="sxs-lookup"><span data-stu-id="b675b-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="b675b-157">**Подсеть**: subnet1</span><span class="sxs-lookup"><span data-stu-id="b675b-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b675b-158">Замените &lt;имя кластера > с именем hello использовалась при создании кластера HDInsight hello в предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="b675b-158">Replace &lt;Cluster name> with hello name you used when creating hello HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="b675b-159">При использовании этих значений hello виртуальная машина размещается в hello же виртуальной сети и подсети, что и кластер HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b675b-159">Using these values, hello virtual machine is placed in hello same virtual network and subnet as hello HDInsight cluster.</span></span> <span data-ttu-id="b675b-160">Эта конфигурация позволяет им toodirectly взаимодействовать друг с другом.</span><span class="sxs-lookup"><span data-stu-id="b675b-160">This configuration allows them toodirectly communicate with each other.</span></span> <span data-ttu-id="b675b-161">Нет toocreate способом с пустым граничного узла кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b675b-161">There is a way toocreate an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="b675b-162">Hello граничного узла может быть кластера используется toomanage hello.</span><span class="sxs-lookup"><span data-stu-id="b675b-162">hello edge node can be used toomanage hello cluster.</span></span>  <span data-ttu-id="b675b-163">Подробные сведения см. в статье [Использование пустых граничных узлов в HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="b675b-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="b675b-164">При использовании tooHBase tooconnect приложения Java удаленно, необходимо использовать hello полное доменное имя (FQDN).</span><span class="sxs-lookup"><span data-stu-id="b675b-164">When using a Java application tooconnect tooHBase remotely, you must use hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="b675b-165">toodetermine это, необходимо получить hello подключения DNS-суффикс hello HBase кластера.</span><span class="sxs-lookup"><span data-stu-id="b675b-165">toodetermine this, you must get hello connection-specific DNS suffix of hello HBase cluster.</span></span> <span data-ttu-id="b675b-166">toodo, можно использовать один из следующих методов hello:</span><span class="sxs-lookup"><span data-stu-id="b675b-166">toodo that, you can use one of hello following methods:</span></span>

   * <span data-ttu-id="b675b-167">Используйте Web браузера toomake вызова Ambari:</span><span class="sxs-lookup"><span data-stu-id="b675b-167">Use a Web browser toomake an Ambari call:</span></span>

     <span data-ttu-id="b675b-168">Обзор toohttps: / /&lt;Имя_кластера >.azurehdinsight.net/api/v1/clusters/&lt;Имя_кластера > / размещает? minimal_response = true.</span><span class="sxs-lookup"><span data-stu-id="b675b-168">Browse toohttps://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="b675b-169">Он включает файл JSON со hello DNS-суффиксов.</span><span class="sxs-lookup"><span data-stu-id="b675b-169">It turns a JSON file with hello DNS suffixes.</span></span>
   * <span data-ttu-id="b675b-170">Используйте веб-сайт Ambari hello:</span><span class="sxs-lookup"><span data-stu-id="b675b-170">Use hello Ambari website:</span></span>

     1. <span data-ttu-id="b675b-171">Обзор слишком https://&lt;Имя_кластера >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="b675b-171">Browse too https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="b675b-172">Нажмите кнопку **узлов** hello верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="b675b-172">Click **Hosts** from hello top menu.</span></span>
   * <span data-ttu-id="b675b-173">Используйте вызовы REST перелистывание toomake:</span><span class="sxs-lookup"><span data-stu-id="b675b-173">Use Curl toomake REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="b675b-174">В hello вернул данные нотации объектов JavaScript (JSON), найдите запись «host_name» hello.</span><span class="sxs-lookup"><span data-stu-id="b675b-174">In hello JavaScript Object Notation (JSON) data returned, find hello "host_name" entry.</span></span> <span data-ttu-id="b675b-175">Он содержит hello полное доменное имя для hello узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="b675b-175">It contains hello FQDN for hello nodes in hello cluster.</span></span> <span data-ttu-id="b675b-176">Например:</span><span class="sxs-lookup"><span data-stu-id="b675b-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="b675b-177">Hello часть hello доменных имен, начинающихся с имени кластера hello является hello DNS-суффикс.</span><span class="sxs-lookup"><span data-stu-id="b675b-177">hello portion of hello domain name beginning with hello cluster name is hello DNS suffix.</span></span> <span data-ttu-id="b675b-178">Например, mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="b675b-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="b675b-179">Использование Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b675b-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="b675b-180">Используйте hello, следуя hello tooregister скрипт Azure PowerShell **Get ClusterDetail** функции, которая может быть DNS-суффикс используется tooreturn hello:</span><span class="sxs-lookup"><span data-stu-id="b675b-180">Use hello following Azure PowerShell script tooregister hello **Get-ClusterDetail** function, which can be used tooreturn hello DNS suffix:</span></span>

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
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
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

     <span data-ttu-id="b675b-181">После выполнения скрипта hello Azure PowerShell, используйте hello следующая команда tooreturn hello DNS-суффикс, используя hello **Get ClusterDetail** функции.</span><span class="sxs-lookup"><span data-stu-id="b675b-181">After running hello Azure PowerShell script, use hello following command tooreturn hello DNS suffix by using hello **Get-ClusterDetail** function.</span></span> <span data-ttu-id="b675b-182">При использовании этой команды укажите имя кластера HDInsight HBase, имя и пароль администратора.</span><span class="sxs-lookup"><span data-stu-id="b675b-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="b675b-183">Эта команда возвращает DNS-суффикс hello.</span><span class="sxs-lookup"><span data-stu-id="b675b-183">This command returns hello DNS suffix.</span></span> <span data-ttu-id="b675b-184">Например, **yourclustername.b4.internal.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="b675b-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

<span data-ttu-id="b675b-185">tooverify, hello виртуальной машины могут взаимодействовать с hello кластер HBase, используйте команду hello `ping headnode0.<dns suffix>` hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b675b-185">tooverify that hello virtual machine can communicate with hello HBase cluster, use hello command `ping headnode0.<dns suffix>` from hello virtual machine.</span></span> <span data-ttu-id="b675b-186">Например, ping headnode0.mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="b675b-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="b675b-187">toouse эту информацию в приложении Java, можно выполнить действия hello в [Maven использовать toobuild Java приложений, использующих HBase с HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate приложения.</span><span class="sxs-lookup"><span data-stu-id="b675b-187">toouse this information in a Java application, you can follow hello steps in [Use Maven toobuild Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate an application.</span></span> <span data-ttu-id="b675b-188">приложение hello toohave подключения удаленного сервера HBase tooa, измените hello **hbase-site.xml** файл в этот примере toouse hello полное доменное имя для Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="b675b-188">toohave hello application connect tooa remote HBase server, modify hello **hbase-site.xml** file in this example toouse hello FQDN for Zookeeper.</span></span> <span data-ttu-id="b675b-189">Например:</span><span class="sxs-lookup"><span data-stu-id="b675b-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="b675b-190">Дополнительные сведения о разрешении имен в виртуальных сетях Azure включая то, как toouse собственного DNS-сервера в разделе [разрешения имен (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="b675b-190">For more information about name resolution in Azure virtual networks, including how toouse your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="b675b-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b675b-191">Next steps</span></span>
<span data-ttu-id="b675b-192">В этом учебнике вы узнали, каким образом toocreate кластер HBase.</span><span class="sxs-lookup"><span data-stu-id="b675b-192">In this tutorial, you learned how toocreate an HBase cluster.</span></span> <span data-ttu-id="b675b-193">toolearn более, см.:</span><span class="sxs-lookup"><span data-stu-id="b675b-193">toolearn more, see:</span></span>

* [<span data-ttu-id="b675b-194">Приступая к работе с HDInsight</span><span class="sxs-lookup"><span data-stu-id="b675b-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="b675b-195">Использование пустых граничных узлов в HDInsight</span><span class="sxs-lookup"><span data-stu-id="b675b-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="b675b-196">Настройка репликации HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="b675b-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="b675b-197">Создание кластеров Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="b675b-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="b675b-198">Приступая к работе с HBase с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="b675b-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="b675b-199">Анализ мнений пользователей Twitter с использованием HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="b675b-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="b675b-200">[Обзор виртуальной сети][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="b675b-200">[Virtual Network Overview][vnet-overview]</span></span>

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
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Подробности подготовить новый кластер HBase hello"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Используйте действие скрипта toocustomize кластер HBase"

[azure-preview-portal]: https://portal.azure.com
