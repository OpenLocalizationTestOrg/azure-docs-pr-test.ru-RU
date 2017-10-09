---
title: "aaaHow toodelete кластер HDInsight - Azure | Документы Microsoft"
description: "Сведения о hello различными способами, можно удалить кластер HDInsight."
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
ms.openlocfilehash: 5b9d9a09eecfdcfaed7a1f5ebab440e13bd358b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a><span data-ttu-id="82152-103">Удалить кластер HDInsight с помощью браузера, PowerShell или Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="82152-103">Delete an HDInsight cluster using your browser, PowerShell, or hello Azure CLI</span></span>

<span data-ttu-id="82152-104">Выставление счетов начинается после кластера и останавливается при удалении кластера hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="82152-104">HDInsight cluster billing starts once a cluster is created and stops when hello cluster is deleted.</span></span> <span data-ttu-id="82152-105">Кластеры оплачиваются поминутно, поэтому всегда следует удалять кластер, когда он больше не нужен.</span><span class="sxs-lookup"><span data-stu-id="82152-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="82152-106">В этом документе вы узнаете, как hello toodelete кластера с помощью портала Azure, Azure PowerShell и hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="82152-106">In this document, you learn how toodelete a cluster using hello Azure portal, Azure PowerShell, and hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82152-107">Удаление кластера HDInsight не приводит к удалению hello учетных записей хранилища Azure или хранилища Озера данных связана с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="82152-107">Deleting an HDInsight cluster does not delete hello Azure Storage accounts or Data Lake Store associated with hello cluster.</span></span> <span data-ttu-id="82152-108">Можно повторно использовать данные, хранящиеся в этих служб в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="82152-108">You can reuse data stored in those services in hello future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="82152-109">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="82152-109">Azure portal</span></span>

1. <span data-ttu-id="82152-110">Войдите в toohello [портал Azure](https://portal.azure.com) и выберите кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="82152-110">Log in toohello [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="82152-111">Если ваш HDInsight кластер не закрепленных toohello панели мониторинга, можно поиск по имени, с помощью поля поиска hello.</span><span class="sxs-lookup"><span data-stu-id="82152-111">If your HDInsight cluster is not pinned toohello dashboard, you can search for it by name using hello search field.</span></span>
   
    ![поиск по порталу](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="82152-113">После колонке hello открывается для hello кластера, выберите hello **удалить** значок.</span><span class="sxs-lookup"><span data-stu-id="82152-113">Once hello blade opens for hello cluster, select hello **Delete** icon.</span></span> <span data-ttu-id="82152-114">При появлении запроса выберите **Да** toodelete hello кластера.</span><span class="sxs-lookup"><span data-stu-id="82152-114">When prompted, select **Yes** toodelete hello cluster.</span></span>
   
    ![значок удаления](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="82152-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="82152-116">Azure PowerShell</span></span>

<span data-ttu-id="82152-117">В командной строке PowerShell используйте hello, следующая команда toodelete hello кластера:</span><span class="sxs-lookup"><span data-stu-id="82152-117">From a PowerShell prompt, use hello following command toodelete hello cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="82152-118">Замените **CLUSTERNAME** с hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="82152-118">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="82152-119">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="82152-119">Azure CLI 1.0</span></span>

<span data-ttu-id="82152-120">В строке используйте hello, следуя toodelete hello кластера:</span><span class="sxs-lookup"><span data-stu-id="82152-120">From a prompt, use hello following toodelete hello cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="82152-121">Замените **CLUSTERNAME** с hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="82152-121">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="82152-122">Сейчас Azure CLI 2.0 не поддерживает удаление кластеров HDInsight (31 июля 2017 г.).</span><span class="sxs-lookup"><span data-stu-id="82152-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (July 31, 2017).</span></span>