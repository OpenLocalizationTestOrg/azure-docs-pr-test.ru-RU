---
title: "Новая версия кластера HDInsight tooa aaaUpgrade-Azure | Документы Microsoft"
description: "Узнайте, как tooUpgrade HDInsight кластера tooa более новой версии."
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
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a><span data-ttu-id="c6ab2-103">Обновление кластера tooa более новой версии HDInsight</span><span class="sxs-lookup"><span data-stu-id="c6ab2-103">Upgrade HDInsight cluster tooa newer version</span></span>
<span data-ttu-id="c6ab2-104">преимущества tootake Здравствуйте компонентам последней версии HDInsight, мы рекомендуем использовать обновленный toolatest версия кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-104">tootake advantage of hello latest HDInsight features, we recommend that HDInsight clusters be upgraded toolatest version.</span></span> <span data-ttu-id="c6ab2-105">Выполните hello ниже рекомендации tooupgrade версий кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-105">Follow hello below guidelines tooupgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="c6ab2-106">Поддержка кластеров HDInsight версий 3.2 и 3.3 скоро завершится.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="c6ab2-107">См. дополнительные сведения о [версиях компонентов HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="c6ab2-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="c6ab2-108">Задачи обновления</span><span class="sxs-lookup"><span data-stu-id="c6ab2-108">Upgrade tasks</span></span>
<span data-ttu-id="c6ab2-109">рабочий процесс tooupgrade Hello кластера HDInsight выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-109">hello workflow tooupgrade HDInsight Cluster is as follows.</span></span>

![Схема рабочего процесса](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="c6ab2-111">Прочитайте каждый раздел этого документа toounderstand изменения, которые могут потребоваться при обновлении кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-111">Read each section of this document toounderstand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="c6ab2-112">Создайте кластер как среду тестирования и контроля качества.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="c6ab2-113">Дополнительные сведения о создании кластера см. в разделе [узнать, как toocreate HDInsight под управлением Linux кластеров](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="c6ab2-113">For more information on creating a cluster, see [Learn how toocreate Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="c6ab2-114">Копирование существующих заданий, источники данных и приемники toohello новой среды.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-114">Copy existing jobs, data sources, and sinks toohello new environment.</span></span> <span data-ttu-id="c6ab2-115">В разделе [tooTest копирование данных среды](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-115">See [Copy Data tooTest Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="c6ab2-116">Выполните Проверочное тестирование toomake убедиться, что заданиям работать должным образом на новый кластер hello.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-116">Perform validation testing toomake sure that your jobs work as expected on hello new cluster.</span></span>


<span data-ttu-id="c6ab2-117">После проверки того, что все работает правильно, необходимо запланируйте время простоя для миграции hello.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-117">Once you have verified that everything works as expected, schedule downtime for hello migration.</span></span> <span data-ttu-id="c6ab2-118">Во время этого простоя hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c6ab2-118">During this downtime, do hello following actions:</span></span>

1.  <span data-ttu-id="c6ab2-119">Создайте резервную копию временные данные, хранящиеся локально на узлах кластера hello.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-119">Back up any transient data stored locally on hello cluster nodes.</span></span> <span data-ttu-id="c6ab2-120">Например, к ним могут относиться данные, которые хранятся непосредственно на головном узле.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="c6ab2-121">Удалите существующий кластер hello.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-121">Delete hello existing cluster.</span></span>
3.  <span data-ttu-id="c6ab2-122">Создание кластера hello же виртуальной сети подсеть с последней (или не поддерживаются) HDI версии с помощью hello одно хранилище данных по умолчанию, hello предыдущего кластера.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-122">Create a cluster in hello same VNET subnet with latest (or supported) HDI version using hello same default data store that hello previous cluster used.</span></span> <span data-ttu-id="c6ab2-123">Это позволяет hello нового кластера toocontinue работать с существующие рабочих данных.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-123">This allows hello new cluster toocontinue working against your existing production data.</span></span>
4.  <span data-ttu-id="c6ab2-124">Импортируйте все временные данные из резервной копии.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="c6ab2-125">Запуск заданий и продолжить обработку с помощью нового кластера hello.</span><span class="sxs-lookup"><span data-stu-id="c6ab2-125">Start jobs/continue processing using hello new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6ab2-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c6ab2-126">Next Steps</span></span>
* [<span data-ttu-id="c6ab2-127">Узнайте, как toocreate HDInsight под управлением Linux кластеров</span><span class="sxs-lookup"><span data-stu-id="c6ab2-127">Learn how toocreate Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="c6ab2-128">Подключиться с помощью SSH tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="c6ab2-128">Connect tooHDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="c6ab2-129">Выполняйте управление кластером под управлением Linux с помощью Ambari</span><span class="sxs-lookup"><span data-stu-id="c6ab2-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

