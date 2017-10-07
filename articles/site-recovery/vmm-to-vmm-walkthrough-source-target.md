---
title: "aaaSet hello исходного и целевого объекта для Hyper-V репликации tooa вторичного сайта с помощью Azure Site Recovery | Документы Microsoft"
description: "Описывает, как tooset вверх hello исходный и целевой при репликации виртуальных машин Hyper-V сайта toosecondary VMM с помощью Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a><span data-ttu-id="c96e2-103">Шаг 6: Настройка hello репликации исходной и целевой</span><span class="sxs-lookup"><span data-stu-id="c96e2-103">Step 6: Set up hello replication source and target</span></span>


<span data-ttu-id="c96e2-104">После создания службы восстановления хранилище для Hyper-V репликации tooa вторичный сайт VMM с [Azure Site Recovery](site-recovery-overview.md), использование этой статьи tooset источник hello и целевые расположения для репликации.</span><span class="sxs-lookup"><span data-stu-id="c96e2-104">After creating a Recovery Services vault for Hyper-V replication tooa secondary VMM site with [Azure Site Recovery](site-recovery-overview.md), use this article tooset up hello source and target replication locations.</span></span> 

<span data-ttu-id="c96e2-105">После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c96e2-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="set-up-hello-source-environment"></a><span data-ttu-id="c96e2-106">Настройка среды источника hello</span><span class="sxs-lookup"><span data-stu-id="c96e2-106">Set up hello source environment</span></span>

<span data-ttu-id="c96e2-107">Установите hello поставщика Azure Site Recovery на серверах VMM и обнаружение и регистрации серверов в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="c96e2-107">Install hello Azure Site Recovery Provider on VMM servers, and discover and register servers in hello vault.</span></span>

1. <span data-ttu-id="c96e2-108">Щелкните **Шаг 1. Подготовка инфраструктуры** > **Источник**.</span><span class="sxs-lookup"><span data-stu-id="c96e2-108">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span>

    ![Настройка источника](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. <span data-ttu-id="c96e2-110">В **Подготовка источника**, нажмите кнопку **+ VMM** tooadd сервера VMM.</span><span class="sxs-lookup"><span data-stu-id="c96e2-110">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![Настройка источника](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. <span data-ttu-id="c96e2-112">В **добавить сервер**, убедитесь, что **System Center VMM server** отображается в **тип сервера** , и этот сервер VMM hello соответствует hello [необходимые компоненты](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="c96e2-112">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites](#prerequisites).</span></span>
4. <span data-ttu-id="c96e2-113">Загрузите файл установки поставщика Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="c96e2-113">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="c96e2-114">Скачайте ключ регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="c96e2-114">Download hello registration key.</span></span> <span data-ttu-id="c96e2-115">Он потребуется при запуске программы установки.</span><span class="sxs-lookup"><span data-stu-id="c96e2-115">You need this when you run setup.</span></span> <span data-ttu-id="c96e2-116">Hello ключ действителен в течение пяти дней после его создания.</span><span class="sxs-lookup"><span data-stu-id="c96e2-116">hello key is valid for five days after you generate it.</span></span>

    ![Настройка источника](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. <span data-ttu-id="c96e2-118">Установите hello поставщика Azure Site Recovery на сервере VMM hello.</span><span class="sxs-lookup"><span data-stu-id="c96e2-118">Install hello Azure Site Recovery Provider on hello VMM server.</span></span> <span data-ttu-id="c96e2-119">Не нужно ничего устанавливать tooexplicitly на серверах узлов Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="c96e2-119">You don't need tooexplicitly install anything on Hyper-V host servers.</span></span>


## <a name="install-hello-azure-site-recovery-provider"></a><span data-ttu-id="c96e2-120">Установка поставщика Azure Site Recovery hello</span><span class="sxs-lookup"><span data-stu-id="c96e2-120">Install hello Azure Site Recovery Provider</span></span>

1. <span data-ttu-id="c96e2-121">Запустите файл установки поставщика hello на каждом сервере VMM.</span><span class="sxs-lookup"><span data-stu-id="c96e2-121">Run hello Provider setup file on each VMM server.</span></span> <span data-ttu-id="c96e2-122">Если VMM развертывается в кластере, следующие hello hello при первом запуске установки:</span><span class="sxs-lookup"><span data-stu-id="c96e2-122">If VMM is deployed in a cluster, do hello following hello first time you install:</span></span>
    -  <span data-ttu-id="c96e2-123">Установите hello поставщик на активном узле и окончания сервера hello установки tooregister hello VMM в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="c96e2-123">Install hello provider on an active node, and finish hello installation tooregister hello VMM server in hello vault.</span></span>
    - <span data-ttu-id="c96e2-124">Затем установите hello поставщика на hello другие узлы.</span><span class="sxs-lookup"><span data-stu-id="c96e2-124">Then, install hello Provider on hello other nodes.</span></span> <span data-ttu-id="c96e2-125">Узлы кластера следует запускать hello ту же версию hello поставщика.</span><span class="sxs-lookup"><span data-stu-id="c96e2-125">Cluster nodes should all run hello same version of hello Provider.</span></span>
2. <span data-ttu-id="c96e2-126">Программа установки выполняет ряд проверок необходимых компонентов и запрашивает разрешение toostop hello VMM службы.</span><span class="sxs-lookup"><span data-stu-id="c96e2-126">Setup runs a few prerequisite checks, and requests permission toostop hello VMM service.</span></span> <span data-ttu-id="c96e2-127">Hello службы VMM будет автоматически перезапущена после завершения программы установки.</span><span class="sxs-lookup"><span data-stu-id="c96e2-127">hello VMM service will be restarted automatically when setup finishes.</span></span> <span data-ttu-id="c96e2-128">При установке на кластере VMM вы запрашиваемые toostop hello кластерной роли.</span><span class="sxs-lookup"><span data-stu-id="c96e2-128">If you install on a VMM cluster, you're prompted toostop hello Cluster role.</span></span>
3. <span data-ttu-id="c96e2-129">В **центра обновления Майкрософт**, вы можете выбрать в toospecify, что поставщик обновления устанавливаются в соответствии с политикой центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c96e2-129">In **Microsoft Update**, you can opt in toospecify that provider updates are installed in accordance with your Microsoft Update policy.</span></span>
4. <span data-ttu-id="c96e2-130">В **установки**, примите или измените расположение установки по умолчанию hello и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="c96e2-130">In **Installation**, accept or modify hello default installation location, and click **Install**.</span></span>

    ![Расположение установки](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. <span data-ttu-id="c96e2-132">После завершения установки нажмите кнопку **зарегистрировать** tooregister hello сервера в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="c96e2-132">After installation is complete, click **Register** tooregister hello server in hello vault.</span></span>

    ![Расположение установки](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. <span data-ttu-id="c96e2-134">В **имя хранилища**, проверьте имя hello hello хранилища, в которых hello будет зарегистрирован сервер.</span><span class="sxs-lookup"><span data-stu-id="c96e2-134">In **Vault name**, verify hello name of hello vault in which hello server will be registered.</span></span> <span data-ttu-id="c96e2-135">Щелкните *Далее*.</span><span class="sxs-lookup"><span data-stu-id="c96e2-135">Click *Next*.</span></span>

    ![Регистрация сервера](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. <span data-ttu-id="c96e2-137">В **подключение к Интернету**, укажите способ подключения hello поставщик, запущенный на сервере VMM hello tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c96e2-137">In **Internet Connection**, specify how hello provider running on hello VMM server connects tooAzure.</span></span>

    ![Параметры Интернета](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - <span data-ttu-id="c96e2-139">Можно указать, поставщик hello следует подключаться напрямую toohello Интернет, или с помощью учетной записи-посредника.</span><span class="sxs-lookup"><span data-stu-id="c96e2-139">You can specify that hello provider should connect directly toohello internet, or via a proxy.</span></span>
   - <span data-ttu-id="c96e2-140">При необходимости задайте параметры прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="c96e2-140">Specify proxy settings if needed.</span></span>
   - <span data-ttu-id="c96e2-141">При использовании прокси-сервер, учетная запись VMM RunAs (DRAProxyAccount) создается автоматически с использованием указанного hello учетные данные прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="c96e2-141">If you use a proxy, a VMM RunAs account (DRAProxyAccount) is created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="c96e2-142">Настройте hello прокси-сервера таким образом, чтобы эта учетная запись успешно проходят проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="c96e2-142">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="c96e2-143">Hello параметры учетной записи запуска от имени можно изменить в консоли VMM hello > **параметры** > **безопасности** > **учетные записи запуска от**.</span><span class="sxs-lookup"><span data-stu-id="c96e2-143">hello RunAs account settings can be modified in hello VMM console > **Settings** > **Security** > **Run As Accounts**.</span></span> <span data-ttu-id="c96e2-144">Перезапустите службы tooupdate hello VMM изменения.</span><span class="sxs-lookup"><span data-stu-id="c96e2-144">Restart hello VMM service tooupdate changes.</span></span>
8. <span data-ttu-id="c96e2-145">В **регистрационный ключ**выберите ключ hello, загружаются из Azure Site Recovery и копируются toohello сервера VMM.</span><span class="sxs-lookup"><span data-stu-id="c96e2-145">In **Registration Key**, select hello key that you downloaded from Azure Site Recovery and copied toohello VMM server.</span></span>
9. <span data-ttu-id="c96e2-146">параметр шифрования Hello используется только при репликации виртуальных машин Hyper-V в облаках tooAzure VMM.</span><span class="sxs-lookup"><span data-stu-id="c96e2-146">hello encryption setting is only used when you're replicating Hyper-V VMs in VMM clouds tooAzure.</span></span> <span data-ttu-id="c96e2-147">Если выполняется репликация tooa вторичного сайта она не используется.</span><span class="sxs-lookup"><span data-stu-id="c96e2-147">If you're replicating tooa secondary site it's not used.</span></span>
10. <span data-ttu-id="c96e2-148">В **имя сервера**, укажите сервер VMM hello tooidentify понятное имя в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="c96e2-148">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="c96e2-149">В конфигурации кластера укажите имя роли кластера VMM hello.</span><span class="sxs-lookup"><span data-stu-id="c96e2-149">In a cluster configuration specify hello VMM cluster role name.</span></span>
11. <span data-ttu-id="c96e2-150">В **синхронизация метаданных облака**выберите, следует ли использовать toosynchronize метаданные для всех облаков на сервере VMM hello hello хранилище.</span><span class="sxs-lookup"><span data-stu-id="c96e2-150">In **Synchronize cloud metadata**, select whether you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="c96e2-151">Это действие нужно только toohappen один раз на каждом сервере.</span><span class="sxs-lookup"><span data-stu-id="c96e2-151">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="c96e2-152">Если вы не хотите toosynchronize все облака, можно не устанавливать флажок и синхронизировать каждое облако отдельно в свойствах облака hello в консоли VMM hello.</span><span class="sxs-lookup"><span data-stu-id="c96e2-152">If you don't want toosynchronize all clouds, you can leave this setting unchecked, and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span>
12. <span data-ttu-id="c96e2-153">Нажмите кнопку **Далее** toocomplete hello процесса.</span><span class="sxs-lookup"><span data-stu-id="c96e2-153">Click **Next** toocomplete hello process.</span></span> <span data-ttu-id="c96e2-154">После регистрации службой Azure Site Recovery извлекает метаданные с сервера VMM hello.</span><span class="sxs-lookup"><span data-stu-id="c96e2-154">After registration, metadata from hello VMM server is retrieved by Azure Site Recovery.</span></span> <span data-ttu-id="c96e2-155">сервер Hello отображается на hello **серверов VMM** вкладку на hello **серверы** страницы в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="c96e2-155">hello server is displayed on hello **VMM Servers** tab on hello **Servers** page in hello vault.</span></span>

    ![сервер;](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. <span data-ttu-id="c96e2-157">После hello сервер доступен в консоли восстановления сайта hello в **источника** > **Подготовка источника** выберите сервер VMM hello и выберите hello облака, в какие hello Hyper-V находится узел.</span><span class="sxs-lookup"><span data-stu-id="c96e2-157">After hello server is available in hello Site Recovery console, in **Source** > **Prepare source** select hello VMM server, and select hello cloud in which hello Hyper-V host is located.</span></span> <span data-ttu-id="c96e2-158">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c96e2-158">Then click **OK**.</span></span>

<span data-ttu-id="c96e2-159">Также можно установить поставщик hello hello командной строке:</span><span class="sxs-lookup"><span data-stu-id="c96e2-159">You can also install hello provider from hello command line:</span></span>

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="c96e2-160">Настройка целевой среды hello</span><span class="sxs-lookup"><span data-stu-id="c96e2-160">Set up hello target environment</span></span>

<span data-ttu-id="c96e2-161">Выберите целевой сервер VMM hello и облака.</span><span class="sxs-lookup"><span data-stu-id="c96e2-161">Select hello target VMM server and cloud:</span></span>

1. <span data-ttu-id="c96e2-162">Нажмите кнопку **подготовки инфраструктуры** > **целевой**и выберите hello целевой сервер VMM требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="c96e2-162">Click **Prepare infrastructure** > **Target**, and select hello target VMM server you want toouse.</span></span>
2. <span data-ttu-id="c96e2-163">Будут отображены облаков на сервере hello, которые синхронизируются с Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="c96e2-163">Clouds on hello server that are synchronized with Site Recovery will be displayed.</span></span> <span data-ttu-id="c96e2-164">Выберите целевое облако hello.</span><span class="sxs-lookup"><span data-stu-id="c96e2-164">Select hello target cloud.</span></span>

   ![Цель](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a><span data-ttu-id="c96e2-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c96e2-166">Next steps</span></span>

<span data-ttu-id="c96e2-167">Go слишком[шаг 7: Настройка сетевого сопоставления](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="c96e2-167">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>
