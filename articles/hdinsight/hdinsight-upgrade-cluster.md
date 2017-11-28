---
title: "Обновление кластера HDInsight до более новой версии в Azure | Документация Майкрософт"
description: "Узнайте, как установить новую версию кластера HDInsight."
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: fa2e37bd922690322ccc3d8f68128180d013b701
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-hdinsight-cluster-to-a-newer-version"></a><span data-ttu-id="22161-103">Обновление кластера HDInsight до более новой версии</span><span class="sxs-lookup"><span data-stu-id="22161-103">Upgrade HDInsight cluster to a newer version</span></span>
<span data-ttu-id="22161-104">Чтобы воспользоваться преимуществами новых возможностей HDInsight, мы рекомендуем обновить кластеры HDInsight до последней версии.</span><span class="sxs-lookup"><span data-stu-id="22161-104">To take advantage of the latest HDInsight features, we recommend that HDInsight clusters be upgraded to latest version.</span></span> <span data-ttu-id="22161-105">Выполните следующие инструкции, чтобы обновить версию кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22161-105">Follow the below guidelines to upgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="22161-106">Поддержка кластеров HDInsight версий 3.2 и 3.3 скоро завершится.</span><span class="sxs-lookup"><span data-stu-id="22161-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="22161-107">См. дополнительные сведения о [версиях компонентов HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="22161-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="22161-108">Задачи обновления</span><span class="sxs-lookup"><span data-stu-id="22161-108">Upgrade tasks</span></span>
<span data-ttu-id="22161-109">Рабочий процесс для обновления кластера HDInsight выглядит так.</span><span class="sxs-lookup"><span data-stu-id="22161-109">The workflow to upgrade HDInsight Cluster is as follows.</span></span>

![Схема рабочего процесса](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="22161-111">Ознакомьтесь со всеми разделами этого документа. Там описаны изменения, которые могут потребоваться при обновлении кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22161-111">Read each section of this document to understand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="22161-112">Создайте кластер как среду тестирования и контроля качества.</span><span class="sxs-lookup"><span data-stu-id="22161-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="22161-113">См. дополнительные сведения о [создании кластеров под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="22161-113">For more information on creating a cluster, see [Learn how to create Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="22161-114">Скопируйте в новую среду существующие задания, источники данных и приемники.</span><span class="sxs-lookup"><span data-stu-id="22161-114">Copy existing jobs, data sources, and sinks to the new environment.</span></span> <span data-ttu-id="22161-115">См. дополнительные сведения о [копировании данных в среду тестирования](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment).</span><span class="sxs-lookup"><span data-stu-id="22161-115">See [Copy Data To Test Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="22161-116">Выполните проверочное тестирование, чтобы убедиться, что задания должным образом работают новом кластере.</span><span class="sxs-lookup"><span data-stu-id="22161-116">Perform validation testing to make sure that your jobs work as expected on the new cluster.</span></span>


<span data-ttu-id="22161-117">Убедившись, что все работает правильно, запланируйте время простоя для миграции.</span><span class="sxs-lookup"><span data-stu-id="22161-117">Once you have verified that everything works as expected, schedule downtime for the migration.</span></span> <span data-ttu-id="22161-118">Во время этого простоя выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="22161-118">During this downtime, do the following actions:</span></span>

1.  <span data-ttu-id="22161-119">Создайте резервную копию всех временных данных, хранящихся локально на узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="22161-119">Back up any transient data stored locally on the cluster nodes.</span></span> <span data-ttu-id="22161-120">Например, к ним могут относиться данные, которые хранятся непосредственно на головном узле.</span><span class="sxs-lookup"><span data-stu-id="22161-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="22161-121">Удалите существующий кластер.</span><span class="sxs-lookup"><span data-stu-id="22161-121">Delete the existing cluster.</span></span>
3.  <span data-ttu-id="22161-122">Создайте кластер в той же подсети виртуальной сети, в которой находится последняя (или поддерживаемая) версия HDI, используя то же хранилище данных по умолчанию, что и для предыдущего кластера.</span><span class="sxs-lookup"><span data-stu-id="22161-122">Create a cluster in the same VNET subnet with latest (or supported) HDI version using the same default data store that the previous cluster used.</span></span> <span data-ttu-id="22161-123">Это позволит новому кластеру продолжить работу с существующими рабочими данными.</span><span class="sxs-lookup"><span data-stu-id="22161-123">This allows the new cluster to continue working against your existing production data.</span></span>
4.  <span data-ttu-id="22161-124">Импортируйте все временные данные из резервной копии.</span><span class="sxs-lookup"><span data-stu-id="22161-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="22161-125">Запустите задания и продолжите обработку с помощью нового кластера.</span><span class="sxs-lookup"><span data-stu-id="22161-125">Start jobs/continue processing using the new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22161-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="22161-126">Next Steps</span></span>
* [<span data-ttu-id="22161-127">Узнайте, как создавать кластеры HDInsight под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="22161-127">Learn how to create Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* <span data-ttu-id="22161-128">[Подключитесь к HDInsight с помощью протокола SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="22161-128">[Connect to HDInsight using SSH](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* [<span data-ttu-id="22161-129">Выполняйте управление кластером под управлением Linux с помощью Ambari</span><span class="sxs-lookup"><span data-stu-id="22161-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

