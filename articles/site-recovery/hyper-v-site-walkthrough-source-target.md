---
title: "aaaSet hello исходного и целевого объекта для tooAzure репликации Hyper-V (без System Center VMM) с Azure Site Recovery | Документы Microsoft"
description: "Перечислены tooset действия hello исходных и целевых параметров репликации хранилища tooAzure виртуальных машин Hyper-V с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a><span data-ttu-id="cbcbb-103">Шаг 8: Настройка hello исходной и целевой для tooAzure репликации Hyper-V</span><span class="sxs-lookup"><span data-stu-id="cbcbb-103">Step 8: Set up hello source and target for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="cbcbb-104">В этой статье описывается, как tooconfigure источника и целевых параметров при репликации локально tooAzure Hyper-V виртуальных машин (без System Center VMM), с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-104">This article describes how tooconfigure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="cbcbb-105">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="cbcbb-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="cbcbb-106">Настройка среды источника hello</span><span class="sxs-lookup"><span data-stu-id="cbcbb-106">Set up hello source environment</span></span>

<span data-ttu-id="cbcbb-107">Настройка сайта hello Hyper-V и установки hello поставщика Azure Site Recovery и агента служб восстановления Azure hello на узлах Hyper-V зарегистрировать узел hello в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-107">Set up hello Hyper-V site, install hello Azure Site Recovery Provider and hello Azure Recovery Services agent on Hyper-V hosts, and register hello site in hello vault.</span></span>

1. <span data-ttu-id="cbcbb-108">В разделе **Подготовка инфраструктуры** щелкните **Источник**.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="cbcbb-109">Щелкните новый узел Hyper-V как контейнер для узлов Hyper-V или кластеры tooadd **+ сайт Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-109">tooadd a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![Настройка источника](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="cbcbb-111">В **узла Hyper-V, создайте**, укажите имя для сайта hello.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-111">In **Create Hyper-V site**, specify a name for hello site.</span></span> <span data-ttu-id="cbcbb-112">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-112">Then click **OK**.</span></span> <span data-ttu-id="cbcbb-113">Теперь выберите hello сайт создан и нажмите кнопку **+ Hyper-V Server** tooadd toohello узла на сервере.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-113">Now, select hello site you created, and click **+Hyper-V Server** tooadd a server toohello site.</span></span>

    ![Настройка источника](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="cbcbb-115">Убедитесь, что **сервер Hyper-V** отображается в разделе **Добавить сервер** > **Тип сервера**.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="cbcbb-116">Убедитесь, что этот сервер hello Hyper-V, требуется tooadd соответствует hello [необходимых компонентов](#on-premises-prerequisites), и является может tooaccess hello указанного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-116">Make sure that hello Hyper-V server you want tooadd complies with hello [prerequisites](#on-premises-prerequisites), and is able tooaccess hello specified URLs.</span></span>
    - <span data-ttu-id="cbcbb-117">Загрузите файл установки поставщика Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-117">Download hello Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="cbcbb-118">Запустите этот файл tooinstall hello поставщика и hello агента служб восстановления на каждом узле Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-118">You run this file tooinstall hello Provider and hello Recovery Services agent on each Hyper-V host.</span></span>

    ![Настройка источника](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a><span data-ttu-id="cbcbb-120">Установите hello поставщика и агента</span><span class="sxs-lookup"><span data-stu-id="cbcbb-120">Install hello Provider and agent</span></span>

1. <span data-ttu-id="cbcbb-121">Запустите файл установки поставщика hello на каждом узле вы добавили сайта toohello Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-121">Run hello Provider setup file on each host you added toohello Hyper-V site.</span></span> <span data-ttu-id="cbcbb-122">Если установка выполняется в кластер Hyper-V, программу установки необходимо запустить на каждом узле кластера.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="cbcbb-123">Установка и регистрация всех узлов кластера Hyper-V гарантирует, что виртуальные машины будут защищены даже при переносе между узлами.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="cbcbb-124">Обновления можно включить на странице **Центр обновления Майкрософт**. Это позволит устанавливать обновления поставщика в соответствии с политикой Центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="cbcbb-125">В **установки**примите или измените расположение установки поставщика по умолчанию hello и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-125">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="cbcbb-126">В **параметры хранилища**, нажмите кнопку **Обзор** tooselect hello хранилище ключей загруженный файл.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-126">In **Vault Settings**, click **Browse** tooselect hello vault key file that you downloaded.</span></span> <span data-ttu-id="cbcbb-127">Укажите подписку Azure Site Recovery hello, имя хранилища hello, и принадлежит hello Hyper-V сайта toowhich hello Hyper-V server.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-127">Specify hello Azure Site Recovery subscription, hello vault name, and hello Hyper-V site toowhich hello Hyper-V server belongs.</span></span>

    ![Регистрация сервера](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="cbcbb-129">В **параметры прокси-сервера**, укажите, как поставщик, запущенный на узлах Hyper-V подключается tooAzure Site Recovery через hello hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-129">In **Proxy Settings**, specify how hello Provider running on Hyper-V hosts connects tooAzure Site Recovery over hello internet.</span></span>

    * <span data-ttu-id="cbcbb-130">Если выбирается tooconnect hello поставщика непосредственно **подключаться напрямую tooAzure Site Recovery без учетной записи-посредника**.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-130">If you want hello Provider tooconnect directly select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="cbcbb-131">Если требуется toouse настраиваемого прокси-сервера для соединения с поставщиком hello существующего прокси-сервер требует проверки подлинности, выберите **подключения tooAzure Site Recovery с использованием прокси-сервер**.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-131">If your existing proxy requires authentication, or you want toouse a custom proxy for hello Provider connection, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="cbcbb-132">При использовании прокси-сервера:</span><span class="sxs-lookup"><span data-stu-id="cbcbb-132">If you use a proxy:</span></span>
        - <span data-ttu-id="cbcbb-133">Укажите адрес hello, порт и учетные данные</span><span class="sxs-lookup"><span data-stu-id="cbcbb-133">Specify hello address, port, and credentials</span></span>
        - <span data-ttu-id="cbcbb-134">Убедитесь, что hello URL-адреса, описанные в hello [необходимые компоненты](#prerequisites) разрешены через прокси-сервер hello.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-134">Make sure hello URLs described in hello [prerequisites](#prerequisites) are allowed through hello proxy.</span></span>

    ![Интернет](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="cbcbb-136">После завершения установки, нажмите кнопку **зарегистрировать** tooregister hello сервера в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-136">After installation finishes, click **Register** tooregister hello server in hello vault.</span></span>

    ![Расположение установки](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="cbcbb-138">После завершения регистрации Azure Site Recovery извлекает метаданные с сервера hello Hyper-V, и hello сервера отображается в **инфраструктура Site Recovery** > **узлов Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-138">After registration finishes, metadata from hello Hyper-V server is retrieved by Azure Site Recovery, and hello server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="cbcbb-139">Настройка целевой среды hello</span><span class="sxs-lookup"><span data-stu-id="cbcbb-139">Set up hello target environment</span></span>

<span data-ttu-id="cbcbb-140">Укажите учетную запись хранилища Azure hello для репликации и hello toowhich сети Azure виртуальные машины Azure будут подключаться после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-140">Specify hello Azure storage account for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="cbcbb-141">Выберите **Подготовка инфраструктуры** > **Цель**.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="cbcbb-142">Выберите подписку hello и hello группы ресурсов, в котором нужно toocreate hello виртуальные машины Azure после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-142">Select hello subscription and hello resource group in which you want toocreate hello Azure VMs after failover.</span></span> <span data-ttu-id="cbcbb-143">Выберите hello развертывания модели, что требуется toouse в Azure (классического или ресурса управления) для hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-143">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello VMs.</span></span>

3. <span data-ttu-id="cbcbb-144">Site Recovery проверяет наличие одной или нескольких совместимых учетных записей хранения и сетей Azure.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="cbcbb-145">Если у вас нет учетной записи хранилища, нажмите кнопку **+ хранилище** toocreate встроенный диспетчер ресурсов на основе учетной записи.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-145">If you don't have a storage account, click **+Storage** toocreate a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="cbcbb-146">Если у вас нет сети Azure, щелкните **+ сети** toocreate встроенного сети на основе диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cbcbb-146">If you don't have a Azure network, click **+Network** toocreate a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="cbcbb-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cbcbb-147">Next steps</span></span>

<span data-ttu-id="cbcbb-148">Go слишком[шаг 9: настроить политику репликации](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="cbcbb-148">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
