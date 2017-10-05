---
title: "Управление кластерами Hadoop с помощью Azure CLI — Azure HDInsight | Документы Майкрософт"
description: "Узнайте, как управлять кластерами Hadoop в Azure HDInsight с помощью интерфейса командной строки Azure. Azure CLI работает в Windows, Mac и Linux."
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
ms.openlocfilehash: 0ee9f2f28978b207dcaf8f77950bd82a897d3fd1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-the-azure-cli"></a><span data-ttu-id="6a036-104">Управление кластерами Hadoop в HDInsight с помощью интерфейса командной строки (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="6a036-104">Manage Hadoop clusters in HDInsight using the Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="6a036-105">Узнайте, как использовать [интерфейс командной строки Azure](../cli-install-nodejs.md) для управления кластерами Hadoop в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6a036-105">Learn how to use the [Azure Command-line Interface](../cli-install-nodejs.md) to manage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="6a036-106">Интерфейс командной строки (CLI) Azure реализован в Node.js.</span><span class="sxs-lookup"><span data-stu-id="6a036-106">The Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="6a036-107">Его можно использовать на любой платформе, которая поддерживает Node.js, включая Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="6a036-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="6a036-108">В этой статье описывается только использование CLI Azure с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6a036-108">This article covers only using the Azure CLI with HDInsight.</span></span> <span data-ttu-id="6a036-109">Общее руководство по использованию Azure CLI см. в статье [Установка и настройка Azure CLI][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="6a036-109">For a general guide on how to use Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="6a036-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6a036-110">Prerequisites</span></span>
<span data-ttu-id="6a036-111">Перед началом работы с этой статьей необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="6a036-111">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="6a036-112">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="6a036-112">**An Azure subscription**.</span></span> <span data-ttu-id="6a036-113">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="6a036-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="6a036-114">**Интерфейс командной строки Azure CLI** — сведения об установке и настройке CLI Azure см. в статье [Установка Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6a036-114">**Azure CLI** - See [Install and configure the Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="6a036-115">**Подключитесь к Azure**, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="6a036-115">**Connect to Azure**, using the following command:</span></span>
  
        azure login
  
    <span data-ttu-id="6a036-116">Дополнительные сведения об аутентификации с помощью рабочей или учебной учетной записи см. в статье [Подключение к среде Azure с использованием интерфейса командной строки Azure (Azure CLI)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="6a036-116">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="6a036-117">**Переключитесь в режим диспетчера ресурсов Azure**с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="6a036-117">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="6a036-118">Чтобы получить справку, используйте параметр **-h** .</span><span class="sxs-lookup"><span data-stu-id="6a036-118">To get help, use the **-h** switch.</span></span>  <span data-ttu-id="6a036-119">Например:</span><span class="sxs-lookup"><span data-stu-id="6a036-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-the-cli"></a><span data-ttu-id="6a036-120">Создание кластеров с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="6a036-120">Create clusters with the CLI</span></span>
<span data-ttu-id="6a036-121">Дополнительные сведения см. в статье [Создание кластеров HDInsight с помощью интерфейса командной строки Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6a036-121">See [Create clusters in HDInsight using the Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="6a036-122">Отображение сведений о кластере</span><span class="sxs-lookup"><span data-stu-id="6a036-122">List and show cluster details</span></span>
<span data-ttu-id="6a036-123">Используйте следующие команды для отображения сведений о кластере:</span><span class="sxs-lookup"><span data-stu-id="6a036-123">Use the following commands to list and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="6a036-124">![Представление командной строки списка кластеров][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="6a036-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="6a036-125">Удаление кластеров</span><span class="sxs-lookup"><span data-stu-id="6a036-125">Delete clusters</span></span>
<span data-ttu-id="6a036-126">Используйте следующую команду для удаления кластера:</span><span class="sxs-lookup"><span data-stu-id="6a036-126">Use the following command to delete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="6a036-127">Можно также удалить кластер, удалив группу ресурсов, которая содержит этот кластер.</span><span class="sxs-lookup"><span data-stu-id="6a036-127">You can also delete a cluster by deleting the resource group that contains the cluster.</span></span> <span data-ttu-id="6a036-128">Обратите внимание, это приведет к удалению всех ресурсов в группе, включая учетную запись хранения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6a036-128">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="6a036-129">Масштабирование кластеров</span><span class="sxs-lookup"><span data-stu-id="6a036-129">Scale clusters</span></span>
<span data-ttu-id="6a036-130">Изменение размера кластера Hadoop</span><span class="sxs-lookup"><span data-stu-id="6a036-130">To change the Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="6a036-131">Включение или отключение доступа по протоколу HTTP для кластера</span><span class="sxs-lookup"><span data-stu-id="6a036-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="6a036-132">Включение или отключение доступа по протоколу RDP для кластера</span><span class="sxs-lookup"><span data-stu-id="6a036-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="6a036-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6a036-133">Next steps</span></span>
<span data-ttu-id="6a036-134">В этой статье вы узнали, как выполнять различные административные задачи в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6a036-134">In this article, you have learned how to perform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="6a036-135">Для получения дополнительных сведений ознакомьтесь со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="6a036-135">To learn more, see the following articles:</span></span>

* <span data-ttu-id="6a036-136">[Администрирование HDInsight с помощью портала Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="6a036-136">[Administer HDInsight by using the Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="6a036-137">[Управление кластерами Hadoop в HDInsight с помощью Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="6a036-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="6a036-138">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="6a036-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="6a036-139">[Установка Azure CLI][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="6a036-139">[How to use the Azure CLI][azure-command-line-tools]</span></span>

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
