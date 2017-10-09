---
title: "aaaSet hello исходного и целевого объекта для tooAzure репликации Hyper-V (с помощью System Center VMM) с Azure Site Recovery | Документы Microsoft"
description: "Перечислены tooset действия hello исходных и целевых параметров репликации виртуальных машин Hyper-V в хранилище tooAzure облака VMM с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: 3f8c5386cb64527c775aef636980bac098ee9905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-with-vmm-replication-tooazure"></a><span data-ttu-id="30266-103">Шаг 8: Настройка hello исходной и целевой для tooAzure репликации Hyper-V (с помощью VMM)</span><span class="sxs-lookup"><span data-stu-id="30266-103">Step 8: Set up hello source and target for Hyper-V (with VMM) replication tooAzure</span></span>

<span data-ttu-id="30266-104">После [Создание хранилища](vmm-to-azure-walkthrough-create-vault.md) и указания теми, которые хотите tooreplicate, использующие этот источник tooconfigure статьи и целевой настройки при репликации виртуальных машин Hyper-V локально в диспетчере виртуальных машин System Center (VMM) tooAzure облаков, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="30266-104">After [creating a vault](vmm-to-azure-walkthrough-create-vault.md) and specifying what you want tooreplicate, use this article tooconfigure source and target settings when replicating on-premises Hyper-V virtual machines in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="30266-105">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="30266-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="30266-106">Настройка среды источника hello</span><span class="sxs-lookup"><span data-stu-id="30266-106">Set up hello source environment</span></span>

<span data-ttu-id="30266-107">S1.</span><span class="sxs-lookup"><span data-stu-id="30266-107">S1.</span></span> <span data-ttu-id="30266-108">Выберите **Подготовка инфраструктуры** > **Источник**.</span><span class="sxs-lookup"><span data-stu-id="30266-108">Click **Prepare Infrastructure** > **Source**.</span></span>

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. <span data-ttu-id="30266-109">В **Подготовка источника**, нажмите кнопку **+ VMM** tooadd сервера VMM.</span><span class="sxs-lookup"><span data-stu-id="30266-109">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![Настройка источника](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="30266-111">В **добавить сервер**, убедитесь, что **System Center VMM server** отображается в **тип сервера** , и этот сервер VMM hello соответствует hello [предварительные условия и URL-адрес требования к](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="30266-111">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites and URL requirements](#prerequisites).</span></span>
4. <span data-ttu-id="30266-112">Загрузите файл установки поставщика Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="30266-112">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="30266-113">Скачайте ключ регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="30266-113">Download hello registration key.</span></span> <span data-ttu-id="30266-114">Он потребуется при запуске программы установки.</span><span class="sxs-lookup"><span data-stu-id="30266-114">You need this when you run setup.</span></span> <span data-ttu-id="30266-115">Hello ключ действителен в течение пяти дней после его создания.</span><span class="sxs-lookup"><span data-stu-id="30266-115">hello key is valid for five days after you generate it.</span></span>

    ![Настройка источника](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-hello-provider-on-hello-vmm-server"></a><span data-ttu-id="30266-117">Установка hello поставщика на сервере VMM hello</span><span class="sxs-lookup"><span data-stu-id="30266-117">Install hello Provider on hello VMM server</span></span>

1. <span data-ttu-id="30266-118">Запустите файл установки поставщика hello на сервере VMM hello.</span><span class="sxs-lookup"><span data-stu-id="30266-118">Run hello Provider setup file on hello VMM server.</span></span>
2. <span data-ttu-id="30266-119">Обновления можно включить на странице **Центр обновления Майкрософт**. Это позволит устанавливать обновления поставщика в соответствии с политикой Центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="30266-119">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="30266-120">В **установки**примите или измените расположение установки поставщика по умолчанию hello и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="30266-120">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>

    ![Расположение установки](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. <span data-ttu-id="30266-122">По завершении установки нажмите кнопку **зарегистрировать** tooregister hello VMM-сервера в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="30266-122">When installation finishes, click **Register** tooregister hello VMM server in hello vault.</span></span>
5. <span data-ttu-id="30266-123">В hello **параметры хранилища** щелкните **Обзор** файл ключа хранилища hello tooselect.</span><span class="sxs-lookup"><span data-stu-id="30266-123">In hello **Vault Settings** page, click **Browse** tooselect hello vault key file.</span></span> <span data-ttu-id="30266-124">Укажите подписку Azure Site Recovery hello и имя хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="30266-124">Specify hello Azure Site Recovery subscription and hello vault name.</span></span>

    ![Регистрация сервера](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. <span data-ttu-id="30266-126">В **подключение к Интернету**, укажите, каким образом поставщик, запущенный на сервере VMM hello связь tooSite восстановления через hello hello internet.</span><span class="sxs-lookup"><span data-stu-id="30266-126">In **Internet Connection**, specify how hello Provider running on hello VMM server will connect tooSite Recovery over hello internet.</span></span>

   * <span data-ttu-id="30266-127">Поставщик tooconnect hello напрямую, установите **подключаться напрямую tooAzure Site Recovery без учетной записи-посредника**.</span><span class="sxs-lookup"><span data-stu-id="30266-127">If you want hello Provider tooconnect directly, select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
   * <span data-ttu-id="30266-128">Если существующий прокси-сервер требует проверки подлинности, либо требуется toouse настраиваемого прокси-сервера, выберите **подключения tooAzure Site Recovery с использованием прокси-сервер**.</span><span class="sxs-lookup"><span data-stu-id="30266-128">If your existing proxy requires authentication, or you want toouse a custom proxy, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
   * <span data-ttu-id="30266-129">При использовании настраиваемого прокси-сервера, укажите адрес hello, порт и учетные данные.</span><span class="sxs-lookup"><span data-stu-id="30266-129">If you use a custom proxy, specify hello address, port, and credentials.</span></span>
   * <span data-ttu-id="30266-130">Если вы используете учетную запись-посредник, должны уже разрешены hello URL-адреса, описанной в [необходимых компонентов](#on-premises-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="30266-130">If you're using a proxy, you should have already allowed hello URLs described in [prerequisites](#on-premises-prerequisites).</span></span>
   * <span data-ttu-id="30266-131">При использовании настраиваемого прокси-сервера, учетная запись VMM RunAs (DRAProxyAccount) будет создана автоматически с помощью указанного hello учетные данные прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="30266-131">If you use a custom proxy, a VMM RunAs account (DRAProxyAccount) will be created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="30266-132">Настройте hello прокси-сервера таким образом, чтобы эта учетная запись успешно проходят проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="30266-132">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="30266-133">можно изменить параметры учетной записи запуска от имени VMM Hello в консоли VMM hello.</span><span class="sxs-lookup"><span data-stu-id="30266-133">hello VMM RunAs account settings can be modified in hello VMM console.</span></span> <span data-ttu-id="30266-134">В **параметры**, разверните **безопасности** > **учетные записи запуска от**, а затем измените hello пароль для DRAProxyAccount.</span><span class="sxs-lookup"><span data-stu-id="30266-134">In **Settings**, expand **Security** > **Run As Accounts**, and then modify hello password for DRAProxyAccount.</span></span> <span data-ttu-id="30266-135">Служба VMM hello toorestart потребуется, чтобы этот параметр вступает в силу.</span><span class="sxs-lookup"><span data-stu-id="30266-135">You’ll need toorestart hello VMM service so that this setting takes effect.</span></span>

     ![Интернет](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. <span data-ttu-id="30266-137">Примите или измените расположение hello SSL-сертификат, который создается автоматически для шифрования данных.</span><span class="sxs-lookup"><span data-stu-id="30266-137">Accept or modify hello location of an SSL certificate that’s automatically generated for data encryption.</span></span> <span data-ttu-id="30266-138">Этот сертификат используется в том случае, если включить шифрование данных для облака, защищаемого платформой Azure на портале Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="30266-138">This certificate is used if you enable data encryption for a cloud protected by Azure in hello Azure Site Recovery portal.</span></span> <span data-ttu-id="30266-139">Сертификат следует хранить в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="30266-139">Keep this certificate safe.</span></span> <span data-ttu-id="30266-140">При запуске tooAzure отработки отказа необходимо его toodecrypt, если включено шифрование данных.</span><span class="sxs-lookup"><span data-stu-id="30266-140">When you run a failover tooAzure you’ll need it toodecrypt, if data encryption is enabled.</span></span>
8. <span data-ttu-id="30266-141">В **имя сервера**, укажите сервер VMM hello tooidentify понятное имя в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="30266-141">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="30266-142">В конфигурации кластера укажите имя роли кластера VMM hello.</span><span class="sxs-lookup"><span data-stu-id="30266-142">In a cluster configuration, specify hello VMM cluster role name.</span></span>
9. <span data-ttu-id="30266-143">Включить **синхронизация метаданных облака**, если вы хотите toosynchronize метаданные для всех облаков на сервере VMM hello hello хранилище.</span><span class="sxs-lookup"><span data-stu-id="30266-143">Enable **Sync cloud metadata**, if you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="30266-144">Это действие нужно только toohappen один раз на каждом сервере.</span><span class="sxs-lookup"><span data-stu-id="30266-144">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="30266-145">Если вы не хотите toosynchronize все облака, можно не устанавливать флажок и синхронизировать каждое облако отдельно в свойствах облака hello в консоли VMM hello.</span><span class="sxs-lookup"><span data-stu-id="30266-145">If you don't want toosynchronize all clouds, you can leave this setting unchecked and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span> <span data-ttu-id="30266-146">Нажмите кнопку **зарегистрировать** toocomplete hello процесса.</span><span class="sxs-lookup"><span data-stu-id="30266-146">Click **Register** toocomplete hello process.</span></span>

    ![Регистрация сервера](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. <span data-ttu-id="30266-148">Начнется процедура регистрации.</span><span class="sxs-lookup"><span data-stu-id="30266-148">Registration starts.</span></span> <span data-ttu-id="30266-149">После завершения регистрации сервера hello отображается в **инфраструктура Site Recovery** > **серверов VMM**.</span><span class="sxs-lookup"><span data-stu-id="30266-149">After registration finishes, hello server is displayed in **Site Recovery Infrastructure** > **VMM Servers**.</span></span>


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a><span data-ttu-id="30266-150">Установка агента служб восстановления Azure hello на узлах Hyper-V</span><span class="sxs-lookup"><span data-stu-id="30266-150">Install hello Azure Recovery Services agent on Hyper-V hosts</span></span>

1. <span data-ttu-id="30266-151">После настройки hello поставщика требуется файл установки hello toodownload для агента служб восстановления Azure hello.</span><span class="sxs-lookup"><span data-stu-id="30266-151">After you've set up hello Provider, you need toodownload hello installation file for hello Azure Recovery Services agent.</span></span> <span data-ttu-id="30266-152">Запустите программу установки на каждом сервере Hyper-V в облаке VMM hello.</span><span class="sxs-lookup"><span data-stu-id="30266-152">Run setup on each Hyper-V server in hello VMM cloud.</span></span>

    ![Сайты Hyper-V](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. <span data-ttu-id="30266-154">В разделе **Проверка предварительных требований** нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="30266-154">In **Prerequisites Check**, click **Next**.</span></span> <span data-ttu-id="30266-155">Все отсутствующие предварительные требования будут установлены автоматически.</span><span class="sxs-lookup"><span data-stu-id="30266-155">Any missing prerequisites will be automatically installed.</span></span>

    ![Предварительные требования для агента служб восстановления](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. <span data-ttu-id="30266-157">В **параметры установки**примите или измените расположение установки hello и расположение кэша hello.</span><span class="sxs-lookup"><span data-stu-id="30266-157">In **Installation Settings**, accept or modify hello installation location, and hello cache location.</span></span> <span data-ttu-id="30266-158">Можно настроить hello кэша на диске, не менее 5 ГБ объема хранилища, но мы рекомендуем дискового кэша более 600 ГБ свободного места.</span><span class="sxs-lookup"><span data-stu-id="30266-158">You can configure hello cache on a drive that has at least 5 GB of storage available but we recommend a cache drive with 600 GB or more of free space.</span></span> <span data-ttu-id="30266-159">Нажмите **Install**(Установить).</span><span class="sxs-lookup"><span data-stu-id="30266-159">Then click **Install**.</span></span>
4. <span data-ttu-id="30266-160">После завершения установки нажмите кнопку **закрыть** toofinish.</span><span class="sxs-lookup"><span data-stu-id="30266-160">After installation is complete, click **Close** toofinish.</span></span>

    ![Регистрация агента служб восстановления Microsoft Azure](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a><span data-ttu-id="30266-162">Установка из командной строки</span><span class="sxs-lookup"><span data-stu-id="30266-162">Command line installation</span></span>
<span data-ttu-id="30266-163">Hello агента служб восстановления Microsoft Azure можно установить из командной строки с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="30266-163">You can install hello Microsoft Azure Recovery Services Agent from command line using hello following command:</span></span>

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a><span data-ttu-id="30266-164">Настройка tooSite доступа к прокси-сервера Интернета восстановления из узлов Hyper-V</span><span class="sxs-lookup"><span data-stu-id="30266-164">Set up internet proxy access tooSite Recovery from Hyper-V hosts</span></span>

<span data-ttu-id="30266-165">агент служб восстановления Hello, работающих на узлах Hyper-V должен tooAzure доступ в Интернет для репликации виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="30266-165">hello Recovery Services agent running on Hyper-V hosts needs internet access tooAzure for VM replication.</span></span> <span data-ttu-id="30266-166">Если вы обращаетесь hello Интернет через прокси, настроить его следующим образом:</span><span class="sxs-lookup"><span data-stu-id="30266-166">If you're accessing hello internet through a proxy, set it up as follows:</span></span>

1. <span data-ttu-id="30266-167">Откройте hello Microsoft Azure Backup MMC оснастку на узле Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="30266-167">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host.</span></span> <span data-ttu-id="30266-168">По умолчанию для быстрого архивации Microsoft Azure доступен с рабочего стола hello или C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="30266-168">By default, a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="30266-169">В оснастке hello, нажмите кнопку **изменить свойства**.</span><span class="sxs-lookup"><span data-stu-id="30266-169">In hello snap-in, click **Change Properties**.</span></span>
3. <span data-ttu-id="30266-170">На hello **конфигурация прокси-сервера** укажите сведения о сервере прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="30266-170">On hello **Proxy Configuration** tab, specify proxy server information.</span></span>

    ![Регистрация агента служб восстановления Microsoft Azure](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. <span data-ttu-id="30266-172">Проверьте, что hello агент может достигать hello URL-адреса, описанные в hello [необходимых компонентов](#on-premises-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="30266-172">Check that hello agent can reach hello URLs described in hello [prerequisites](#on-premises-prerequisites).</span></span>

## <a name="set-up-hello-target-environment"></a><span data-ttu-id="30266-173">Настройка целевой среды hello</span><span class="sxs-lookup"><span data-stu-id="30266-173">Set up hello target environment</span></span>
<span data-ttu-id="30266-174">Укажите toobe учетной записи хранилища Azure hello, используемым для репликации и hello toowhich сети Azure виртуальные машины Azure будут подключаться после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="30266-174">Specify hello Azure storage account toobe used for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="30266-175">Нажмите кнопку **подготовки инфраструктуры** > **целевой**, выберите подписку hello и hello группы ресурсов, место toocreate hello отработку отказа виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="30266-175">Click **Prepare infrastructure** > **Target**, select hello subscription and hello resource group where you want toocreate hello failed over virtual machines.</span></span> <span data-ttu-id="30266-176">Выберите модель развертывания hello, toouse в Azure (классического или ресурса управления), необходимый для hello отработку отказа виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="30266-176">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello failed over virtual machines.</span></span>

    ![Хранилище](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. <span data-ttu-id="30266-178">Site Recovery проверяет наличие одной или нескольких совместимых учетных записей хранения и сетей Azure.</span><span class="sxs-lookup"><span data-stu-id="30266-178">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    ![Хранилище](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. <span data-ttu-id="30266-180">Если вы еще не создали учетную запись хранилища, и требуется toocreate один с помощью диспетчера ресурсов, щелкните **+ учетная запись хранения** toodo этой встроенной.</span><span class="sxs-lookup"><span data-stu-id="30266-180">If you haven't created a storage account, and you want toocreate one using Resource Manager, click **+Storage account** toodo that inline.</span></span>  <span data-ttu-id="30266-181">На hello **создать учетную запись хранения** колонке укажите имя учетной записи, тип, подписки и расположения.</span><span class="sxs-lookup"><span data-stu-id="30266-181">On hello **Create storage account** blade specify an account name, type, subscription, and location.</span></span> <span data-ttu-id="30266-182">Учетная запись Hello должна находиться в hello местоположения hello в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="30266-182">hello account should be in hello same location as hello Recovery Services vault.</span></span>

   ![Хранилище](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * <span data-ttu-id="30266-184">Если вы хотите toocreate учетной записи хранилища с помощью классической модели hello, сделать это в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="30266-184">If you want toocreate a storage account using hello classic model, do that in hello Azure portal.</span></span> [<span data-ttu-id="30266-185">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="30266-185">Learn more</span></span>](../storage/common/storage-create-storage-account.md)
   * <span data-ttu-id="30266-186">Если вы используете учетную запись хранения premium для реплицируемых данных, настройте дополнительная Стандартная учетная запись хранения, toostore журналов репликации, захватывающих данные локальной tooon текущие изменения.</span><span class="sxs-lookup"><span data-stu-id="30266-186">If you’re using a premium storage account for replicated data, set up an additional standard storage account, toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
5. <span data-ttu-id="30266-187">Если вы еще не создали сети Azure, и требуется toocreate один с помощью диспетчера ресурсов, щелкните **+ сети** toodo этой встроенной.</span><span class="sxs-lookup"><span data-stu-id="30266-187">If you haven't created an Azure network, and you want toocreate one using Resource Manager, click **+Network** toodo that inline.</span></span> <span data-ttu-id="30266-188">На hello **Создание виртуальной сети** колонке укажите сетевое имя, диапазон адресов, сведения о подсети, подписки и расположения.</span><span class="sxs-lookup"><span data-stu-id="30266-188">On hello **Create virtual network** blade specify a network name, address range, subnet details, subscription, and location.</span></span> <span data-ttu-id="30266-189">сеть Hello должны находиться в hello местоположения hello в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="30266-189">hello network should be in hello same location as hello Recovery Services vault.</span></span>

   ![Сеть](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   <span data-ttu-id="30266-191">Если вы хотите toocreate сети с помощью классической модели hello, сделать это в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="30266-191">If you want toocreate a network using hello classic model, do that in hello Azure portal.</span></span> <span data-ttu-id="30266-192">[Подробнее](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="30266-192">[Learn more](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span>





## <a name="next-steps"></a><span data-ttu-id="30266-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="30266-193">Next steps</span></span>

<span data-ttu-id="30266-194">Go слишком[шаг 9: настройте сетевое сопоставление](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="30266-194">Go too[Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>
