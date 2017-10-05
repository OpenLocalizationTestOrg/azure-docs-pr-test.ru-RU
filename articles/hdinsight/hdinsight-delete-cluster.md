---
title: "Удаление кластера HDInsight в Azure | Документы Майкрософт"
description: "Сведения о различных способах удаления кластера HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 65dac529df15d2dd43eec17673d82a2832f7692e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-the-azure-cli"></a><span data-ttu-id="491f4-103">Удаление кластера HDInsight с помощью браузера, PowerShell или Azure CLI</span><span class="sxs-lookup"><span data-stu-id="491f4-103">Delete an HDInsight cluster using your browser, PowerShell, or the Azure CLI</span></span>

<span data-ttu-id="491f4-104">Начисление оплаты начинается после создания кластера HDInsight и прекращается только после его удаления.</span><span class="sxs-lookup"><span data-stu-id="491f4-104">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span></span> <span data-ttu-id="491f4-105">Кластеры оплачиваются поминутно, поэтому всегда следует удалять кластер, когда он больше не нужен.</span><span class="sxs-lookup"><span data-stu-id="491f4-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="491f4-106">В этом документе вы узнаете, как удалить кластер с помощью портала Azure, Azure PowerShell и Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="491f4-106">In this document, you learn how to delete a cluster using the Azure portal, Azure PowerShell, and the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="491f4-107">При удалении кластера HDInsight не происходит удаление связанных с ним учетных записей хранения Azure или Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="491f4-107">Deleting an HDInsight cluster does not delete the Azure Storage accounts or Data Lake Store associated with the cluster.</span></span> <span data-ttu-id="491f4-108">Данные, хранящиеся в этих службах, можно повторно использовать в будущем.</span><span class="sxs-lookup"><span data-stu-id="491f4-108">You can reuse data stored in those services in the future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="491f4-109">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="491f4-109">Azure portal</span></span>

1. <span data-ttu-id="491f4-110">Войдите на [портал Azure](https://portal.azure.com) и выберите свой кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="491f4-110">Log in to the [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="491f4-111">Если кластер HDInsight не закреплен на панели мониторинга, его можно найти по имени с помощью поля поиска.</span><span class="sxs-lookup"><span data-stu-id="491f4-111">If your HDInsight cluster is not pinned to the dashboard, you can search for it by name using the search field.</span></span>
   
    ![поиск по порталу](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="491f4-113">Открыв колонку кластера, выберите значок **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="491f4-113">Once the blade opens for the cluster, select the **Delete** icon.</span></span> <span data-ttu-id="491f4-114">При появлении запроса выберите **Да**, чтобы удалить кластер.</span><span class="sxs-lookup"><span data-stu-id="491f4-114">When prompted, select **Yes** to delete the cluster.</span></span>
   
    ![значок удаления](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="491f4-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="491f4-116">Azure PowerShell</span></span>

<span data-ttu-id="491f4-117">Введите следующую команду в командной строке PowerShell, чтобы удалить кластер.</span><span class="sxs-lookup"><span data-stu-id="491f4-117">From a PowerShell prompt, use the following command to delete the cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="491f4-118">Замените **CLUSTERNAME** именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="491f4-118">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="491f4-119">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="491f4-119">Azure CLI 1.0</span></span>

<span data-ttu-id="491f4-120">Введите следующую команду в командной строке, чтобы удалить кластер.</span><span class="sxs-lookup"><span data-stu-id="491f4-120">From a prompt, use the following to delete the cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="491f4-121">Замените **CLUSTERNAME** именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="491f4-121">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="491f4-122">Сейчас Azure CLI 2.0 не поддерживает удаление кластеров HDInsight (31 июля 2017 г.).</span><span class="sxs-lookup"><span data-stu-id="491f4-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (July 31, 2017).</span></span>