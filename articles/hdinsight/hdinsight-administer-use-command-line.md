---
title: "aaaManage Hadoop кластеры, использующие Azure CLI - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как кластеров toouse hello интерфейса командной строки Azure toomanage Hadoop в Azure HDInsight. Hello Azure CLI работает в Windows, Mac и Linux."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 03b0cff9331c1c581095b80cc6d1177d843ffa83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a><span data-ttu-id="c2bec-104">Управление кластерами Hadoop в HDInsight с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c2bec-104">Manage Hadoop clusters in HDInsight using hello Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="c2bec-105">Узнайте, как toouse hello [интерфейса командной строки Azure](../cli-install-nodejs.md) toomanage Hadoop кластеров в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c2bec-105">Learn how toouse hello [Azure Command-line Interface](../cli-install-nodejs.md) toomanage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="c2bec-106">Hello Azure CLI реализуется в Node.js.</span><span class="sxs-lookup"><span data-stu-id="c2bec-106">hello Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="c2bec-107">Его можно использовать на любой платформе, которая поддерживает Node.js, включая Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="c2bec-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="c2bec-108">В этой статье рассматриваются только с помощью hello Azure CLI с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c2bec-108">This article covers only using hello Azure CLI with HDInsight.</span></span> <span data-ttu-id="c2bec-109">Общие инструкции о том, как toouse Azure CLI см. в разделе [установить и настроить Azure CLI][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="c2bec-109">For a general guide on how toouse Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="c2bec-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c2bec-110">Prerequisites</span></span>
<span data-ttu-id="c2bec-111">Прежде чем приступать к этой статье, необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="c2bec-111">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="c2bec-112">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="c2bec-112">**An Azure subscription**.</span></span> <span data-ttu-id="c2bec-113">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="c2bec-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="c2bec-114">**Azure CLI** -разделе [установить и настроить hello Azure CLI](../cli-install-nodejs.md) сведения об установке и настройке.</span><span class="sxs-lookup"><span data-stu-id="c2bec-114">**Azure CLI** - See [Install and configure hello Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="c2bec-115">**Подключение tooAzure**, с использованием hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c2bec-115">**Connect tooAzure**, using hello following command:</span></span>
  
        azure login
  
    <span data-ttu-id="c2bec-116">Дополнительные сведения о проверке подлинности с помощью рабочей или учебной учетной записи см. в разделе [подключение tooan подписки Azure из hello Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="c2bec-116">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="c2bec-117">**Переключите режим диспетчера ресурсов Azure toohello**, с использованием hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c2bec-117">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="c2bec-118">Справка tooget использовать hello **-h** переключения.</span><span class="sxs-lookup"><span data-stu-id="c2bec-118">tooget help, use hello **-h** switch.</span></span>  <span data-ttu-id="c2bec-119">Например:</span><span class="sxs-lookup"><span data-stu-id="c2bec-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a><span data-ttu-id="c2bec-120">Создать кластеры с hello CLI</span><span class="sxs-lookup"><span data-stu-id="c2bec-120">Create clusters with hello CLI</span></span>
<span data-ttu-id="c2bec-121">В разделе [создание кластеров HDInsight с помощью hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c2bec-121">See [Create clusters in HDInsight using hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="c2bec-122">Отображение сведений о кластере</span><span class="sxs-lookup"><span data-stu-id="c2bec-122">List and show cluster details</span></span>
<span data-ttu-id="c2bec-123">Используйте следующие команды toolist hello и отображают сведения о кластере:</span><span class="sxs-lookup"><span data-stu-id="c2bec-123">Use hello following commands toolist and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="c2bec-124">![Представление командной строки списка кластеров][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="c2bec-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="c2bec-125">Удаление кластеров</span><span class="sxs-lookup"><span data-stu-id="c2bec-125">Delete clusters</span></span>
<span data-ttu-id="c2bec-126">Используйте следующие команды toodelete кластера hello:</span><span class="sxs-lookup"><span data-stu-id="c2bec-126">Use hello following command toodelete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="c2bec-127">Можно также удалить кластер, удалив hello группы ресурсов, содержащий hello кластера.</span><span class="sxs-lookup"><span data-stu-id="c2bec-127">You can also delete a cluster by deleting hello resource group that contains hello cluster.</span></span> <span data-ttu-id="c2bec-128">Обратите внимание, это приведет к удалению всех ресурсов группы hello, включая учетную запись хранения по умолчанию hello hello.</span><span class="sxs-lookup"><span data-stu-id="c2bec-128">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="c2bec-129">Масштабирование кластеров</span><span class="sxs-lookup"><span data-stu-id="c2bec-129">Scale clusters</span></span>
<span data-ttu-id="c2bec-130">hello toochange размер кластера Hadoop:</span><span class="sxs-lookup"><span data-stu-id="c2bec-130">toochange hello Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="c2bec-131">Включение или отключение доступа по протоколу HTTP для кластера</span><span class="sxs-lookup"><span data-stu-id="c2bec-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="c2bec-132">Включение или отключение доступа по протоколу RDP для кластера</span><span class="sxs-lookup"><span data-stu-id="c2bec-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="c2bec-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c2bec-133">Next steps</span></span>
<span data-ttu-id="c2bec-134">В этой статье вы узнали как tooperform разные HDInsight кластер задачи администрирования.</span><span class="sxs-lookup"><span data-stu-id="c2bec-134">In this article, you have learned how tooperform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="c2bec-135">toolearn более, см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="c2bec-135">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="c2bec-136">[Администрирование HDInsight с помощью портала Azure hello][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="c2bec-136">[Administer HDInsight by using hello Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="c2bec-137">[Управление кластерами Hadoop в HDInsight с помощью Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="c2bec-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="c2bec-138">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="c2bec-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="c2bec-139">[Как toouse hello Azure CLI][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="c2bec-139">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "Отображение кластеров"
