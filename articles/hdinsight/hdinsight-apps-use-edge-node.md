---
title: "aaaUse пустые краевым узлам на кластеров Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Как tooadd edge пустой узел tooan HDInsight кластер, который можно использовать в качестве клиента и затем теста или узла приложения HDInsight."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: 9c910905b51f2fe92e6e5d47d86a32bd5247c2cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="3680e-103">Использование пустых граничных узлов в кластерах Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="3680e-103">Use empty edge nodes on Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="3680e-104">Узнайте, как tooadd пустой ребро кластера HDInsight tooan узла.</span><span class="sxs-lookup"><span data-stu-id="3680e-104">Learn how tooadd an empty edge node tooan HDInsight cluster.</span></span> <span data-ttu-id="3680e-105">Пустой граничного узла — это виртуальная машина Linux с hello же клиентские средства установлен и настроен как hello headnodes, но ни одна служба Hadoop под управлением.</span><span class="sxs-lookup"><span data-stu-id="3680e-105">An empty edge node is a Linux virtual machine with hello same client tools installed and configured as in hello headnodes, but with no Hadoop services running.</span></span> <span data-ttu-id="3680e-106">Hello граничного узла можно использовать для доступа к кластеру hello, тестирования клиентские приложения и размещение клиентских приложений.</span><span class="sxs-lookup"><span data-stu-id="3680e-106">You can use hello edge node for accessing hello cluster, testing your client applications, and hosting your client applications.</span></span> 

<span data-ttu-id="3680e-107">При создании кластера hello, можно добавить существующий кластер HDInsight edge пустой узел tooan, tooa новый кластер.</span><span class="sxs-lookup"><span data-stu-id="3680e-107">You can add an empty edge node tooan existing HDInsight cluster, tooa new cluster when you create hello cluster.</span></span> <span data-ttu-id="3680e-108">Добавление пустого граничного узла осуществляется с помощью шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3680e-108">Adding an empty edge node is done using Azure Resource Manager template.</span></span>  <span data-ttu-id="3680e-109">Hello следующий пример демонстрирует, как это можно сделать с помощью шаблона:</span><span class="sxs-lookup"><span data-stu-id="3680e-109">hello following sample demonstrates how it is done using a template:</span></span>

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

<span data-ttu-id="3680e-110">Как показано в образце hello, при необходимости можно вызвать [записать действие в скрипт](hdinsight-hadoop-customize-cluster-linux.md) tooperform дополнительной настройки, таких как установка [оттенка Apache](hdinsight-hadoop-hue-linux.md) в hello граничного узла.</span><span class="sxs-lookup"><span data-stu-id="3680e-110">As shown in hello sample, you can optionally call a [script action](hdinsight-hadoop-customize-cluster-linux.md) tooperform additional configuration, such as installing [Apache Hue](hdinsight-hadoop-hue-linux.md) in hello edge node.</span></span> <span data-ttu-id="3680e-111">сценарий действие Hello сценарий должен быть общедоступным Интернете hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-111">hello script action script must be publicly accessible on hello web.</span></span>  <span data-ttu-id="3680e-112">Например если сценарий hello хранится в хранилище Azure, используйте общедоступных контейнеров или общедоступных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="3680e-112">For example, if hello script is stored in Azure storage, use either public containers or public blobs.</span></span>

<span data-ttu-id="3680e-113">размер виртуальной машины узел edge Hello требования hello HDInsight кластера рабочий узел виртуальной машины размера.</span><span class="sxs-lookup"><span data-stu-id="3680e-113">hello edge node virtual machine size must meet hello HDInsight cluster worker node vm size requirements.</span></span> <span data-ttu-id="3680e-114">Hello рекомендуется работника размеры виртуальных машин на узле, см. в разделе [кластеров создать Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="3680e-114">For hello recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>

<span data-ttu-id="3680e-115">После создания граничного узла можно подключиться toohello граничного узла с помощью SSH и запустить клиент кластера Hadoop hello tooaccess средства в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3680e-115">After you have created an edge node, you can connect toohello edge node using SSH, and run client tools tooaccess hello Hadoop cluster in HDInsight.</span></span>

> [!WARNING] 
> <span data-ttu-id="3680e-116">Возможность использования пустого граничного узла с HDInsight доступна в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="3680e-116">Using an empty edge node with HDInsight is currently in preview.</span></span> <span data-ttu-id="3680e-117">Пользовательские компоненты, установленные на hello граничного узла получать ограниченную техническую поддержку от Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3680e-117">Custom components that are installed on hello edge node receive commercially reasonable support from Microsoft.</span></span> <span data-ttu-id="3680e-118">В результате могут быть устранены возникающие проблемы.</span><span class="sxs-lookup"><span data-stu-id="3680e-118">This might result in resolving problems you encounter.</span></span> <span data-ttu-id="3680e-119">Или может быть ссылка toocommunity ресурсы для получения дополнительной помощи.</span><span class="sxs-lookup"><span data-stu-id="3680e-119">Or you may be referred toocommunity resources for further assistance.</span></span> <span data-ttu-id="3680e-120">Hello ниже приведены некоторые hello большинство активными узлами для получения справки из hello сообщества:</span><span class="sxs-lookup"><span data-stu-id="3680e-120">hello following are some of hello most active sites for getting help from hello community:</span></span>
>
> * [<span data-ttu-id="3680e-121">Форум MSDN для HDInsight</span><span class="sxs-lookup"><span data-stu-id="3680e-121">MSDN forum for HDInsight</span></span>](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * <span data-ttu-id="3680e-122">[http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="3680e-122">[http://stackoverflow.com](http://stackoverflow.com).</span></span>
>
> <span data-ttu-id="3680e-123">При использовании технологии Apache может быть помощника может toofind через hello сайтов проектов Apache на [http://apache.org](http://apache.org), такие как hello [Hadoop](http://hadoop.apache.org/) сайта.</span><span class="sxs-lookup"><span data-stu-id="3680e-123">If you are using an Apache technology, you may be able toofind assistance through hello Apache project sites on [http://apache.org](http://apache.org), such as hello [Hadoop](http://hadoop.apache.org/) site.</span></span>

## <a name="add-an-edge-node-tooan-existing-cluster"></a><span data-ttu-id="3680e-124">Добавить существующий кластер узла tooan edge</span><span class="sxs-lookup"><span data-stu-id="3680e-124">Add an edge node tooan existing cluster</span></span>
<span data-ttu-id="3680e-125">В этом разделе используется tooadd шаблона диспетчера ресурсов edge узел tooan существующий кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3680e-125">In this section, you use a Resource Manager template tooadd an edge node tooan existing HDInsight cluster.</span></span>  <span data-ttu-id="3680e-126">шаблон диспетчера ресурсов Hello можно найти в [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/).</span><span class="sxs-lookup"><span data-stu-id="3680e-126">hello Resource Manager template can be found in [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/).</span></span> <span data-ttu-id="3680e-127">шаблон диспетчера ресурсов Hello вызывает действие скрипта, расположенный в https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. сценарий Hello не выполняет каких-либо действий.</span><span class="sxs-lookup"><span data-stu-id="3680e-127">hello Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. hello script doesn't perform any actions.</span></span>  <span data-ttu-id="3680e-128">Это toodemonstrate вызов действия скрипта из шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3680e-128">It is toodemonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="3680e-129">**tooadd tooan edge пустой узел существующего кластера**</span><span class="sxs-lookup"><span data-stu-id="3680e-129">**tooadd an empty edge node tooan existing cluster**</span></span>

1. <span data-ttu-id="3680e-130">Создайте кластер HDInsight, если его еще нет.</span><span class="sxs-lookup"><span data-stu-id="3680e-130">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="3680e-131">Ознакомьтесь со статьей [Руководство по Hadoop. Приступая к работе с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3680e-131">See [Hadoop tutorial: Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="3680e-132">Щелкните hello toosign образа в tooAzure и откройте hello шаблона диспетчера ресурсов Azure в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3680e-132">Click hello following image toosign in tooAzure and open hello Azure Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. <span data-ttu-id="3680e-133">Настройте hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="3680e-133">Configure hello following properties:</span></span>
   
   * <span data-ttu-id="3680e-134">**Подписки**: выберите подписку Azure, используемый для создания кластера hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-134">**Subscription**: Select an Azure subscription used for creating hello cluster.</span></span>
   * <span data-ttu-id="3680e-135">**Группа ресурсов**: hello выберите группы ресурсов, используемой для hello существующего кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3680e-135">**Resource group**: Select hello resource group used for hello existing HDInsight cluster.</span></span>
   * <span data-ttu-id="3680e-136">**Расположение**: выберите расположение hello hello существующего кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3680e-136">**Location**: Select hello location of hello existing HDInsight cluster.</span></span>
   * <span data-ttu-id="3680e-137">**Имя кластера**: Введите имя существующего кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-137">**Cluster Name**: Enter hello name of an existing HDInsight cluster.</span></span>
   * <span data-ttu-id="3680e-138">**Ребро размер узла**: выберите один из размеров виртуальных Машин hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-138">**Edge Node Size**: Select one of hello VM sizes.</span></span> <span data-ttu-id="3680e-139">Hello размер виртуальной машины должны соответствовать требованиям к размеру hello рабочих узла виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="3680e-139">hello vm size must meet hello worker node vm size requirements.</span></span> <span data-ttu-id="3680e-140">Hello рекомендуется работника размеры виртуальных машин на узле, см. в разделе [кластеров создать Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="3680e-140">For hello recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>
   * <span data-ttu-id="3680e-141">**Ребро префикса узла**: hello значение по умолчанию — **новый**.</span><span class="sxs-lookup"><span data-stu-id="3680e-141">**Edge Node Prefix**: hello default value is **new**.</span></span>  <span data-ttu-id="3680e-142">Используется значение по умолчанию hello, является имя узла edge hello **новый edgenode**.</span><span class="sxs-lookup"><span data-stu-id="3680e-142">Using hello default value, hello edge node name is **new-edgenode**.</span></span>  <span data-ttu-id="3680e-143">Можно настроить префикс hello из портала hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-143">You can customize hello prefix from hello portal.</span></span> <span data-ttu-id="3680e-144">Можно также настроить hello полное имя из шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-144">You can also customize hello full name from hello template.</span></span>

4. <span data-ttu-id="3680e-145">Проверьте **я принимаю условия, указанных выше, toohello**, а затем нажмите кнопку **покупки** toocreate hello граничного узла.</span><span class="sxs-lookup"><span data-stu-id="3680e-145">Check **I agree toohello terms and conditions stated above**, and then click  **Purchase** toocreate hello edge node.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="3680e-146">Убедитесь, что группы ресурсов Azure hello tooselect hello существующих кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3680e-146">Make sure tooselect hello Azure resource group for hello existing HDInsight cluster.</span></span>  <span data-ttu-id="3680e-147">В противном случае ошибки hello сообщение «Невозможно выполнить запрошенную операцию для вложенных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3680e-147">Otherwise, you get hello error message "Can not perform requested operation on nested resource.</span></span> <span data-ttu-id="3680e-148">Родительский ресурс &lt;ClusterName> не найден."</span><span class="sxs-lookup"><span data-stu-id="3680e-148">Parent resource '&lt;ClusterName>' not found."</span></span>

## <a name="add-an-edge-node-when-creating-a-cluster"></a><span data-ttu-id="3680e-149">Добавление граничного узла при создании кластера</span><span class="sxs-lookup"><span data-stu-id="3680e-149">Add an edge node when creating a cluster</span></span>
<span data-ttu-id="3680e-150">В этом разделе можно использовать диспетчер ресурсов шаблона toocreate HDInsight с граничного узла.</span><span class="sxs-lookup"><span data-stu-id="3680e-150">In this section, you use a Resource Manager template toocreate HDInsight cluster with an edge node.</span></span>  <span data-ttu-id="3680e-151">шаблон диспетчера ресурсов Hello можно найти в hello [коллекции шаблонов быстрый запуск Azure](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span><span class="sxs-lookup"><span data-stu-id="3680e-151">hello Resource Manager template can be found in hello [Azure QuickStart Templates gallery](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span></span> <span data-ttu-id="3680e-152">шаблон диспетчера ресурсов Hello вызывает действие скрипта, расположенный в https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. сценарий Hello не выполняет каких-либо действий.</span><span class="sxs-lookup"><span data-stu-id="3680e-152">hello Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. hello script doesn't perform any actions.</span></span>  <span data-ttu-id="3680e-153">Это toodemonstrate вызов действия скрипта из шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3680e-153">It is toodemonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="3680e-154">**tooadd tooan edge пустой узел существующего кластера**</span><span class="sxs-lookup"><span data-stu-id="3680e-154">**tooadd an empty edge node tooan existing cluster**</span></span>

1. <span data-ttu-id="3680e-155">Создайте кластер HDInsight, если его еще нет.</span><span class="sxs-lookup"><span data-stu-id="3680e-155">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="3680e-156">Ознакомьтесь со статьей [Руководство по Hadoop. Приступая к работе с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3680e-156">See [Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="3680e-157">Щелкните hello toosign образа в tooAzure и откройте hello шаблона диспетчера ресурсов Azure в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3680e-157">Click hello following image toosign in tooAzure and open hello Azure Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. <span data-ttu-id="3680e-158">Настройте hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="3680e-158">Configure hello following properties:</span></span>
   
   * <span data-ttu-id="3680e-159">**Подписки**: выберите подписку Azure, используемый для создания кластера hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-159">**Subscription**: Select an Azure subscription used for creating hello cluster.</span></span>
   * <span data-ttu-id="3680e-160">**Группа ресурсов**: создать новую группу ресурсов, используемых для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="3680e-160">**Resource group**: Create a new resource group used for hello cluster.</span></span>
   * <span data-ttu-id="3680e-161">**Расположение**: выберите расположение для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-161">**Location**: Select a location for hello resource group.</span></span>
   * <span data-ttu-id="3680e-162">**Имя кластера**: Введите имя для нового кластера toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-162">**Cluster Name**: Enter a name for hello new cluster toocreate.</span></span>
   * <span data-ttu-id="3680e-163">**Имя входа пользователя кластера**: Введите имя пользователя Hadoop HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-163">**Cluster Login User Name**: Enter hello Hadoop HTTP user name.</span></span>  <span data-ttu-id="3680e-164">имя по умолчанию Hello — **администратора**.</span><span class="sxs-lookup"><span data-stu-id="3680e-164">hello default name is **admin**.</span></span>
   * <span data-ttu-id="3680e-165">**Имя входа пароль кластера**: Введите пароль пользователя Hadoop HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-165">**Cluster Login Password**: Enter hello Hadoop HTTP user password.</span></span>
   * <span data-ttu-id="3680e-166">**SSH имя пользователя**: Введите имя пользователя SSH hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-166">**Ssh User Name**: Enter hello SSH user name.</span></span> <span data-ttu-id="3680e-167">имя по умолчанию Hello — **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="3680e-167">hello default name is **sshuser**.</span></span>
   * <span data-ttu-id="3680e-168">**SSH пароль**: Введите пароль пользователя для SSH hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-168">**Ssh Password**: Enter hello SSH user password.</span></span>
   * <span data-ttu-id="3680e-169">**Установите действие сценария**: оставьте значение по умолчанию hello в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="3680e-169">**Install Script Action**: Keep hello default value for going through this tutorial.</span></span>
     
     <span data-ttu-id="3680e-170">Некоторые свойства были жестко задано в шаблоне hello: тип кластера, число узлов кластера рабочих, размер границы узла и имя узла Edge.</span><span class="sxs-lookup"><span data-stu-id="3680e-170">Some properties have been hardcoded in hello template: Cluster type, Cluster worker node count, Edge node size, and Edge node name.</span></span>
4. <span data-ttu-id="3680e-171">Проверьте **я принимаю условия, указанных выше, toohello**и нажмите кнопку **покупки** toocreate hello кластер с граничного узла hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-171">Check **I agree toohello terms and conditions stated above**, and then click  **Purchase** toocreate hello cluster with hello edge node.</span></span>

## <a name="access-an-edge-node"></a><span data-ttu-id="3680e-172">Доступ к граничному узлу</span><span class="sxs-lookup"><span data-stu-id="3680e-172">Access an edge node</span></span>
<span data-ttu-id="3680e-173">Hello граничного узла ssh конечная точка является &lt;EdgeNodeName >.&lt; Имя_кластера >-ssh.azurehdinsight.net:22.</span><span class="sxs-lookup"><span data-stu-id="3680e-173">hello edge node ssh endpoint is &lt;EdgeNodeName>.&lt;ClusterName>-ssh.azurehdinsight.net:22.</span></span>  <span data-ttu-id="3680e-174">Например, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span><span class="sxs-lookup"><span data-stu-id="3680e-174">For example, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span></span>

<span data-ttu-id="3680e-175">Hello граничного узла отображается как приложение на hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3680e-175">hello edge node appears as an application on hello Azure portal.</span></span>  <span data-ttu-id="3680e-176">Hello портала дает hello hello tooaccess сведения ребро узла с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="3680e-176">hello portal gives you hello information tooaccess hello edge node using SSH.</span></span>

<span data-ttu-id="3680e-177">**Конечная точка SSH узел tooverify hello edge**</span><span class="sxs-lookup"><span data-stu-id="3680e-177">**tooverify hello edge node SSH endpoint**</span></span>

1. <span data-ttu-id="3680e-178">Войдите на toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3680e-178">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3680e-179">Откройте hello кластера HDInsight с граничного узла.</span><span class="sxs-lookup"><span data-stu-id="3680e-179">Open hello HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="3680e-180">Нажмите кнопку **приложений** из кластера колонки hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-180">Click **Applications** from hello cluster blade.</span></span> <span data-ttu-id="3680e-181">Должны появиться hello граничного узла.</span><span class="sxs-lookup"><span data-stu-id="3680e-181">You shall see hello edge node.</span></span>  <span data-ttu-id="3680e-182">имя по умолчанию Hello — **новый edgenode**.</span><span class="sxs-lookup"><span data-stu-id="3680e-182">hello default name is **new-edgenode**.</span></span>
4. <span data-ttu-id="3680e-183">Щелкните узел edge hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-183">Click hello edge node.</span></span> <span data-ttu-id="3680e-184">Вы увидите конечной точки для SSH hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-184">You shall see hello SSH endpoint.</span></span>

<span data-ttu-id="3680e-185">**Куст toouse на hello граничного узла**</span><span class="sxs-lookup"><span data-stu-id="3680e-185">**toouse Hive on hello edge node**</span></span>

1. <span data-ttu-id="3680e-186">Используйте SSH tooconnect toohello граничного узла.</span><span class="sxs-lookup"><span data-stu-id="3680e-186">Use SSH tooconnect toohello edge node.</span></span> <span data-ttu-id="3680e-187">См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3680e-187">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="3680e-188">После подключения toohello граничного узла с помощью SSH, используйте следующие командной консоли Hive hello tooopen hello:</span><span class="sxs-lookup"><span data-stu-id="3680e-188">After you have connected toohello edge node using SSH, use hello following command tooopen hello Hive console:</span></span>
   
        hive
3. <span data-ttu-id="3680e-189">Выполните следующие команды tooshow Hive таблицы в кластере hello hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-189">Run hello following command tooshow Hive tables in hello cluster:</span></span>
   
        show tables;

## <a name="delete-an-edge-node"></a><span data-ttu-id="3680e-190">Удаление граничного узла</span><span class="sxs-lookup"><span data-stu-id="3680e-190">Delete an edge node</span></span>
<span data-ttu-id="3680e-191">Граничного узла можно удалить из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3680e-191">You can delete an edge node from hello Azure portal.</span></span>

<span data-ttu-id="3680e-192">**tooaccess граничного узла**</span><span class="sxs-lookup"><span data-stu-id="3680e-192">**tooaccess an edge node**</span></span>

1. <span data-ttu-id="3680e-193">Войдите на toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3680e-193">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3680e-194">Откройте hello кластера HDInsight с граничного узла.</span><span class="sxs-lookup"><span data-stu-id="3680e-194">Open hello HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="3680e-195">Нажмите кнопку **приложений** из кластера колонки hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-195">Click **Applications** from hello cluster blade.</span></span> <span data-ttu-id="3680e-196">Появится список граничных узлов.</span><span class="sxs-lookup"><span data-stu-id="3680e-196">You shall see a list of edge nodes.</span></span>  
4. <span data-ttu-id="3680e-197">Щелкните правой кнопкой мыши hello граничного узла toodelete и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="3680e-197">Right-click hello edge node you want toodelete, and then click **Delete**.</span></span>
5. <span data-ttu-id="3680e-198">Нажмите кнопку **Да** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="3680e-198">Click **Yes** tooconfirm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3680e-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3680e-199">Next steps</span></span>
<span data-ttu-id="3680e-200">В этой статье вы узнали как tooadd граничного узла и как tooaccess hello граничного узла.</span><span class="sxs-lookup"><span data-stu-id="3680e-200">In this article, you have learned how tooadd an edge node and how tooaccess hello edge node.</span></span> <span data-ttu-id="3680e-201">toolearn более, см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-201">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="3680e-202">[Установка приложений HDInsight](hdinsight-apps-install-applications.md): Узнайте, как кластеры tooinstall tooyour HDInsight приложения.</span><span class="sxs-lookup"><span data-stu-id="3680e-202">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how tooinstall an HDInsight application tooyour clusters.</span></span>
* <span data-ttu-id="3680e-203">[Установка пользовательских приложений HDInsight](hdinsight-apps-install-custom-applications.md): Узнайте, как toodeploy неопубликованные приложения tooHDInsight HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3680e-203">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how toodeploy an unpublished HDInsight application tooHDInsight.</span></span>
* <span data-ttu-id="3680e-204">[Публикация приложений HDInsight](hdinsight-apps-publish-applications.md): Узнайте, как toopublish вашего пользовательского tooAzure приложения Marketplace HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3680e-204">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how toopublish your custom HDInsight applications tooAzure Marketplace.</span></span>
* <span data-ttu-id="3680e-205">[MSDN: Установить приложение HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Узнайте, как toodefine HDInsight приложений.</span><span class="sxs-lookup"><span data-stu-id="3680e-205">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how toodefine HDInsight applications.</span></span>
* <span data-ttu-id="3680e-206">[Настроить кластеры HDInsight под управлением Linux, с помощью сценария действия](hdinsight-hadoop-customize-cluster-linux.md): Узнайте, как toouse действие сценария tooinstall дополнительные приложения.</span><span class="sxs-lookup"><span data-stu-id="3680e-206">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how toouse Script Action tooinstall additional applications.</span></span>
* <span data-ttu-id="3680e-207">[Создавать кластеры под управлением Linux Hadoop в HDInsight с помощью шаблонов диспетчера ресурсов](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Узнайте, как кластеры toocreate шаблонов диспетчера ресурсов toocall HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3680e-207">[Create Linux-based Hadoop clusters in HDInsight using Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how toocall Resource Manager templates toocreate HDInsight clusters.</span></span>

