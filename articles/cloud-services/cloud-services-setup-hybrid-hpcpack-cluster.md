---
title: "кластер aaaSet копирование гибридного пакета HPC в Azure | Документы Microsoft"
description: "Узнайте, как toouse пакета Microsoft HPC и Azure tooset вверх небольшой, высокая производительность гибридного вычислительных кластера (HPC)"
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="3ce94-103">Настройка гибридного кластера высокопроизводительных вычислительных систем (HPC) с помощью пакета Microsoft HPC и вычислительных узлов Azure по требованию</span><span class="sxs-lookup"><span data-stu-id="3ce94-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="3ce94-104">Используйте Microsoft HPC Pack 2012 R2 и Azure tooset копирование небольшого гибридного высокопроизводительных вычислительных систем (HPC) кластера.</span><span class="sxs-lookup"><span data-stu-id="3ce94-104">Use Microsoft HPC Pack 2012 R2 and Azure tooset up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="3ce94-105">Hello кластера, приведенными в этой статье состоит из локального головного узла HPC Pack и некоторые вычислительные узлы развертывания по запросу в Azure облачной службы.</span><span class="sxs-lookup"><span data-stu-id="3ce94-105">hello cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span></span> <span data-ttu-id="3ce94-106">Вычислительные задания можно выполнять на hello гибридный кластер.</span><span class="sxs-lookup"><span data-stu-id="3ce94-106">You can then run compute jobs on hello hybrid cluster.</span></span>

![Гибридный кластер высокопроизводительных вычислений (HPC)][Overview] 

<span data-ttu-id="3ce94-108">Это учебник показывает один из подходов, иногда называют кластера «прорыв toohello облако» toouse масштабируемых, по запросу ресурсы Azure toorun ресурсоемких приложений.</span><span class="sxs-lookup"><span data-stu-id="3ce94-108">This tutorial shows one approach, sometimes called cluster "burst toohello cloud," toouse scalable, on-demand Azure resources toorun compute-intensive applications.</span></span>

<span data-ttu-id="3ce94-109">В этом учебнике предполагается, что у читателя нет опыта работы с вычислительными кластерами или пакетом HPC.</span><span class="sxs-lookup"><span data-stu-id="3ce94-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span></span> <span data-ttu-id="3ce94-110">Это предполагаемое только toohelp развертывание гибридный вычислительный кластер быстро для демонстрационных целей.</span><span class="sxs-lookup"><span data-stu-id="3ce94-110">It is intended only toohelp you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="3ce94-111">Рекомендации и шаги toodeploy гибридных HPC Pack кластера с масштабом больше в рабочей среде или toouse 2016 пакета HPC, см. в разделе hello [подробное руководство](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="3ce94-111">For considerations and steps toodeploy a hybrid HPC Pack cluster at greater scale in a production environment, or toouse HPC Pack 2016, see hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="3ce94-112">Другие сценарии использования пакета HPC, включая автоматизированное развертывание кластера в виртуальных машинах Azure, см. в статье [Варианты создания в Azure кластера HPC под управлением Windows и управления им с помощью пакета HPC](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3ce94-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ce94-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3ce94-113">Prerequisites</span></span>
* <span data-ttu-id="3ce94-114">**Подписка Azure.** Если ее нет, можно за пару минут создать [бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="3ce94-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="3ce94-115">**На локальном компьютере под управлением Windows Server 2012 R2 или Windows Server 2012** -использовать этот компьютер в качестве головного узла кластера HPC hello hello.</span><span class="sxs-lookup"><span data-stu-id="3ce94-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as hello head node of hello HPC cluster.</span></span> <span data-ttu-id="3ce94-116">Если вы еще не установили Windows Server, вы можете скачать и установить [ознакомительную версию](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span><span class="sxs-lookup"><span data-stu-id="3ce94-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="3ce94-117">Hello компьютер должен быть присоединены к домену tooan домена Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3ce94-117">hello computer must be joined tooan Active Directory domain.</span></span> <span data-ttu-id="3ce94-118">Для целей тестирования можно настроить компьютере головного узла hello как контроллер домена.</span><span class="sxs-lookup"><span data-stu-id="3ce94-118">For test purposes, you can configure hello head node computer as a domain controller.</span></span> <span data-ttu-id="3ce94-119">tooadd hello роли сервера служб домена Active Directory и повысить уровень компьютера головного узла hello как контроллер домена см. в разделе hello документации по Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3ce94-119">tooadd hello Active Directory Domain Services server role and promote hello head node computer as a domain controller, see hello documentation for Windows Server.</span></span>
  * <span data-ttu-id="3ce94-120">toosupport пакета HPC, hello операционной системы должен быть установлен в одном из этих языков: английский, японский и китайский (упрощенное письмо).</span><span class="sxs-lookup"><span data-stu-id="3ce94-120">toosupport HPC Pack, hello operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="3ce94-121">Убедитесь, что установлены важные и критические обновления.</span><span class="sxs-lookup"><span data-stu-id="3ce94-121">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="3ce94-122">**HPC Pack 2012 R2** - [загрузки](http://go.microsoft.com/fwlink/p/?linkid=328024) hello установочный пакет для последней версии hello без издержек и скопируйте компьютере головного узла hello файлы toohello.</span><span class="sxs-lookup"><span data-stu-id="3ce94-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) hello installation package for hello latest version free of charge and copy hello files toohello head node computer.</span></span> <span data-ttu-id="3ce94-123">Выберите файлы установки в hello же языке, что и установку Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3ce94-123">Choose installation files in hello same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="3ce94-124">Если вы хотите toouse HPC Pack 2016 вместо HPC Pack 2012 R2, требуется дополнительная настройка.</span><span class="sxs-lookup"><span data-stu-id="3ce94-124">If you want toouse HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="3ce94-125">В разделе hello [подробное руководство](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="3ce94-125">See hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="3ce94-126">**Учетная запись домена** -этой учетной записи должны быть настроены права локального администратора на tooinstall hello головного узла HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="3ce94-126">**Domain account** - This account must be configured with local Administrator permissions on hello head node tooinstall HPC Pack.</span></span>
* <span data-ttu-id="3ce94-127">**Подключение TCP на порту 443** из tooAzure hello головного узла.</span><span class="sxs-lookup"><span data-stu-id="3ce94-127">**TCP connectivity on port 443** from hello head node tooAzure.</span></span>

## <a name="install-hpc-pack-on-hello-head-node"></a><span data-ttu-id="3ce94-128">Установка пакета HPC на головном узле hello</span><span class="sxs-lookup"><span data-stu-id="3ce94-128">Install HPC Pack on hello head node</span></span>
<span data-ttu-id="3ce94-129">Сначала установите пакет Microsoft HPC на локальном компьютере под управлением Windows Server,</span><span class="sxs-lookup"><span data-stu-id="3ce94-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span></span> <span data-ttu-id="3ce94-130">Этот компьютер становится hello головного узла кластера hello.</span><span class="sxs-lookup"><span data-stu-id="3ce94-130">This computer becomes hello head node of hello cluster.</span></span>

1. <span data-ttu-id="3ce94-131">Войдите на головном узле toohello, используя учетную запись домена, имеющую права локального администратора.</span><span class="sxs-lookup"><span data-stu-id="3ce94-131">Log on toohello head node by using a domain account that has local Administrator permissions.</span></span>

2. <span data-ttu-id="3ce94-132">Запустите мастер установки пакета HPC hello Setup.exe из файлов установки пакета HPC hello.</span><span class="sxs-lookup"><span data-stu-id="3ce94-132">Start hello HPC Pack Installation Wizard by running Setup.exe from hello HPC Pack installation files.</span></span>

3. <span data-ttu-id="3ce94-133">На hello **установки HPC Pack 2012 R2** щелкните **новую установку или добавьте новые компоненты tooan существующей установки**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-133">On hello **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features tooan existing installation**.</span></span>

    ![Установка пакета HPC 2012][install_hpc1]

4. <span data-ttu-id="3ce94-135">На hello **страницы условия пользовательского соглашения на использование программного обеспечения Microsoft**, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-135">On hello **Microsoft Software User Agreement page**, click **Next**.</span></span>

5. <span data-ttu-id="3ce94-136">На hello **Выбор типа установки** нажмите кнопку **Создание нового кластера HPC, создайте головной узел**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-136">On hello **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>

6. <span data-ttu-id="3ce94-137">несколько тестов предустановки запускается мастер Hello.</span><span class="sxs-lookup"><span data-stu-id="3ce94-137">hello wizard runs several pre-installation tests.</span></span> <span data-ttu-id="3ce94-138">Нажмите кнопку **Далее** на hello **правила установки** страницы, если все тесты пройдены.</span><span class="sxs-lookup"><span data-stu-id="3ce94-138">Click **Next** on hello **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="3ce94-139">В противном случае просмотрите информация hello и внесите необходимые изменения в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="3ce94-139">Otherwise, review hello information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="3ce94-140">Затем выполните тесты hello еще раз или при необходимости запуска hello мастер установки еще раз.</span><span class="sxs-lookup"><span data-stu-id="3ce94-140">Then run hello tests again or if necessary start hello Installation Wizard again.</span></span>
7. <span data-ttu-id="3ce94-141">На hello **конфигурация HPC DB** убедитесь, что **головного узла** выбран для всех баз данных HPC и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-141">On hello **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span> 

    ![Конфигурация базы данных][install_hpc4]

8. <span data-ttu-id="3ce94-143">Примите значения по умолчанию на оставшихся страницах мастера hello hello.</span><span class="sxs-lookup"><span data-stu-id="3ce94-143">Accept default selections on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="3ce94-144">На hello **установить обязательные компоненты** щелкните **установить**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-144">On hello **Install Required Components** page, click **Install**.</span></span>
   
    ![Установить][install_hpc6]

9. <span data-ttu-id="3ce94-146">После завершения установки hello, снимите флажок **запустить диспетчер кластеров HPC** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-146">After hello installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="3ce94-147">(Вы запустите диспетчер кластеров HPC позднее.)</span><span class="sxs-lookup"><span data-stu-id="3ce94-147">(You start HPC Cluster Manager in a later step.)</span></span>
   
    ![Готово][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a><span data-ttu-id="3ce94-149">Подготовка hello подписки Azure</span><span class="sxs-lookup"><span data-stu-id="3ce94-149">Prepare hello Azure subscription</span></span>
<span data-ttu-id="3ce94-150">Выполните следующие шаги в hello hello [портал Azure](https://portal.azure.com) с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce94-150">Perform hello following steps in hello [Azure portal](https://portal.azure.com) with your Azure subscription.</span></span> <span data-ttu-id="3ce94-151">После выполнения этих действий, вы можете развернуть узлы Azure с hello локального головного узла.</span><span class="sxs-lookup"><span data-stu-id="3ce94-151">After completing these steps, you can deploy Azure nodes from hello on-premises head node.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="3ce94-152">Также запишите идентификатор подписки Azure, который понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="3ce94-152">Also make a note of your Azure subscription ID, which you need later.</span></span> <span data-ttu-id="3ce94-153">Найти идентификатор hello в **подписки** hello портала.</span><span class="sxs-lookup"><span data-stu-id="3ce94-153">Find hello ID in **Subscriptions** in hello portal.</span></span>
  > 

### <a name="upload-hello-default-management-certificate"></a><span data-ttu-id="3ce94-154">Отправка сертификата управления по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="3ce94-154">Upload hello default management certificate</span></span>
<span data-ttu-id="3ce94-155">Пакет HPC устанавливает самозаверяющий сертификат на головном узле hello, вызывается hello по умолчанию Microsoft HPC Azure сертификат управления, который можно отправить как сертификат управления Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce94-155">HPC Pack installs a self-signed certificate on hello head node, called hello Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="3ce94-156">Этот сертификат предоставляется для тестирования и hello подтверждение концепции развертываний toosecure hello подключения между головным узлом и Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce94-156">This certificate is provided for testing and proof-of-concept deployments toosecure hello connection between hello head node and Azure.</span></span>

1. <span data-ttu-id="3ce94-157">Головной узел компьютера hello вход toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3ce94-157">From hello head node computer, sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="3ce94-158">Выберите **Подписки** > *имя_вашей_подписки*.</span><span class="sxs-lookup"><span data-stu-id="3ce94-158">Click **Subscriptions** > *your_subscription_name*.</span></span>

3. <span data-ttu-id="3ce94-159">Выберите **Сертификаты управления** > **Отправить**.4.</span><span class="sxs-lookup"><span data-stu-id="3ce94-159">Click **Management certificates** > **Upload**.4.</span></span> <span data-ttu-id="3ce94-160">Перейдите на головной узел hello файл C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer hello.</span><span class="sxs-lookup"><span data-stu-id="3ce94-160">Browse on hello head node for hello file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="3ce94-161">Затем выберите **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-161">Then, click **Upload**.</span></span>

   
<span data-ttu-id="3ce94-162">Hello **по умолчанию управления HPC Azure** сертификат отображается в списке hello сертификатов управления.</span><span class="sxs-lookup"><span data-stu-id="3ce94-162">hello **Default HPC Azure Management** certificate appears in hello list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="3ce94-163">Создание облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="3ce94-163">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="3ce94-164">Для повышения производительности рекомендуется создать облачную службу hello и hello учетной записи хранения (в дальнейшем) в hello одной географической области.</span><span class="sxs-lookup"><span data-stu-id="3ce94-164">For best performance, create hello cloud service and hello storage account (in a later step) in hello same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="3ce94-165">На портале hello щелкните **облачные службы (классические)** > **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-165">In hello portal, click **Cloud services (classic)** > **+Add**.</span></span>

2.  <span data-ttu-id="3ce94-166">Введите имя DNS для службы hello, выберите группу ресурсов и расположение и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-166">Type a DNS name for hello service, choose a resource group and a location, and then click **Create**.</span></span>


### <a name="create-an-azure-storage-account"></a><span data-ttu-id="3ce94-167">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="3ce94-167">Create an Azure storage account</span></span>
1. <span data-ttu-id="3ce94-168">На портале hello щелкните **учетные записи хранения (классические)** > **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-168">In hello portal, click **Storage accounts (classic)** > **+Add**.</span></span>

2. <span data-ttu-id="3ce94-169">Введите имя учетной записи hello и выберите hello **классический** модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="3ce94-169">Type a name for hello account, and select hello **Classic** deployment model.</span></span>

3. <span data-ttu-id="3ce94-170">Выберите группу ресурсов и расположение. Для остальных параметров оставьте значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3ce94-170">Choose a resource group and a location, and leave other settings at default values.</span></span> <span data-ttu-id="3ce94-171">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-171">Then click **Create**.</span></span>

## <a name="configure-hello-head-node"></a><span data-ttu-id="3ce94-172">Настройка головного узла hello</span><span class="sxs-lookup"><span data-stu-id="3ce94-172">Configure hello head node</span></span>
<span data-ttu-id="3ce94-173">toouse toodeploy диспетчера кластеров HPC узлы Azure и задания toosubmit сначала выполнить некоторые действия по настройке кластера требуется.</span><span class="sxs-lookup"><span data-stu-id="3ce94-173">toouse HPC Cluster Manager toodeploy Azure nodes and toosubmit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="3ce94-174">На головном узле hello запустите диспетчер кластеров HPC.</span><span class="sxs-lookup"><span data-stu-id="3ce94-174">On hello head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="3ce94-175">Если hello **Выбор головного узла** диалоговое окно, нажмите кнопку **локального компьютера**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-175">If hello **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="3ce94-176">Hello **списку задач развертывания** отображается.</span><span class="sxs-lookup"><span data-stu-id="3ce94-176">hello **Deployment To-do List** appears.</span></span>

2. <span data-ttu-id="3ce94-177">В разделе **Необходимые задачи развертывания** щелкните **Настроить сеть**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-177">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![Настройка сети][config_hpc2]

3. <span data-ttu-id="3ce94-179">В окне приветствия мастера настройки сети выберите **все узлы только в сети предприятия** (топологии 5).</span><span class="sxs-lookup"><span data-stu-id="3ce94-179">In hello Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span> <span data-ttu-id="3ce94-180">Эта конфигурация сети — hello простой для демонстрационных целей.</span><span class="sxs-lookup"><span data-stu-id="3ce94-180">This network configuration is hello simplest for demonstration purposes.</span></span>
   
    ![Топология 5][config_hpc3]
   
4. <span data-ttu-id="3ce94-182">Нажмите кнопку **Далее** tooaccept значения по умолчанию на оставшихся страницах мастера hello hello.</span><span class="sxs-lookup"><span data-stu-id="3ce94-182">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="3ce94-183">Затем на hello **проверки** щелкните **Настройка** toocomplete hello сетевая конфигурация.</span><span class="sxs-lookup"><span data-stu-id="3ce94-183">Then, on hello **Review** tab, click **Configure** toocomplete hello network configuration.</span></span>

5. <span data-ttu-id="3ce94-184">В hello **списку задач развертывания**, нажмите кнопку **учетные данные установки**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-184">In hello **Deployment To-do List**, click **Provide installation credentials**.</span></span>

6. <span data-ttu-id="3ce94-185">В hello **учетных данных установки** диалоговом hello введите учетные данные учетной записи домена hello использования tooinstall пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="3ce94-185">In hello **Installation Credentials** dialog box, type hello credentials of hello domain account that you used tooinstall HPC Pack.</span></span> <span data-ttu-id="3ce94-186">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-186">Then click **OK**.</span></span> 
   
    ![Учетные данные установки][config_hpc6]
   
7. <span data-ttu-id="3ce94-188">В hello **списку задач развертывания**, нажмите кнопку **настройте именование новых узлов hello**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-188">In hello **Deployment To-do List**, click **Configure hello naming of new nodes**.</span></span>

8. <span data-ttu-id="3ce94-189">В hello **укажите серии именования узлов** диалоговое окно примите именования рядов и нажмите кнопку по умолчанию hello **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-189">In hello **Specify Node Naming Series** dialog box, accept hello default naming series and click **OK**.</span></span> <span data-ttu-id="3ce94-190">Выполнение этого действия, несмотря на то, что hello узлов Azure, добавляемое в этом учебнике присваиваются автоматически.</span><span class="sxs-lookup"><span data-stu-id="3ce94-190">Complete this step even though hello Azure nodes you add in this tutorial are named automatically.</span></span>
   
    ![Именование узлов][config_hpc8]
   
9. <span data-ttu-id="3ce94-192">В hello **списку задач развертывания**, нажмите кнопку **создайте шаблон узла**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-192">In hello **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="3ce94-193">Далее в учебнике hello используйте toohello кластера узлов Azure tooadd hello узла шаблона.</span><span class="sxs-lookup"><span data-stu-id="3ce94-193">Later in hello tutorial, you use hello node template tooadd Azure nodes toohello cluster.</span></span>

10. <span data-ttu-id="3ce94-194">В hello мастер создания шаблона узла, выполните hello следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3ce94-194">In hello Create Node Template Wizard, do hello following:</span></span>
    
    <span data-ttu-id="3ce94-195">а.</span><span class="sxs-lookup"><span data-stu-id="3ce94-195">a.</span></span> <span data-ttu-id="3ce94-196">На hello **выберите тип шаблона узла** щелкните **шаблона узла Windows Azure**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-196">On hello **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span></span>
    
    ![Шаблон узла][config_hpc10]
    
    <span data-ttu-id="3ce94-198">b.</span><span class="sxs-lookup"><span data-stu-id="3ce94-198">b.</span></span> <span data-ttu-id="3ce94-199">Нажмите кнопку **Далее** tooaccept hello по умолчанию имя шаблона.</span><span class="sxs-lookup"><span data-stu-id="3ce94-199">Click **Next** tooaccept hello default template name.</span></span>
    
    <span data-ttu-id="3ce94-200">c.</span><span class="sxs-lookup"><span data-stu-id="3ce94-200">c.</span></span> <span data-ttu-id="3ce94-201">На hello **предоставляют сведения о подписке** введите идентификатор подписки Azure (доступно в сведениях учетной записи Azure).</span><span class="sxs-lookup"><span data-stu-id="3ce94-201">On hello **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="3ce94-202">Затем в разделе **Сертификат управления** найдите **сертификат управления Microsoft HPC Azure по умолчанию.**</span><span class="sxs-lookup"><span data-stu-id="3ce94-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span></span> <span data-ttu-id="3ce94-203">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-203">Then click **Next**.</span></span>
    
    ![Шаблон узла][config_hpc12]
    
    <span data-ttu-id="3ce94-205">d.</span><span class="sxs-lookup"><span data-stu-id="3ce94-205">d.</span></span> <span data-ttu-id="3ce94-206">На hello **предоставляют сведения о службе** страницу, выберите hello облачной службы и учетной записи хранилища hello, созданный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="3ce94-206">On hello **Provide Service Information** page, select hello cloud service and hello storage account that you created in a previous step.</span></span> <span data-ttu-id="3ce94-207">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-207">Then click **Next**.</span></span>
    
    ![Шаблон узла][config_hpc13]
    
    <span data-ttu-id="3ce94-209">д.</span><span class="sxs-lookup"><span data-stu-id="3ce94-209">e.</span></span> <span data-ttu-id="3ce94-210">Нажмите кнопку **Далее** tooaccept значения по умолчанию на оставшихся страницах мастера hello hello.</span><span class="sxs-lookup"><span data-stu-id="3ce94-210">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="3ce94-211">Затем на hello **проверки** щелкните **создать** шаблона узла toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="3ce94-211">Then, on hello **Review** tab, click **Create** toocreate hello node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="3ce94-212">По умолчанию hello шаблона узла Azure включает параметры для toostart (провизионирование) и остановка узлов hello вручную, с помощью диспетчера кластеров HPC.</span><span class="sxs-lookup"><span data-stu-id="3ce94-212">By default, hello Azure node template includes settings for you toostart (provision) and stop hello nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="3ce94-213">При необходимости можно настроить toostart расписание и остановить hello узлов Azure автоматически.</span><span class="sxs-lookup"><span data-stu-id="3ce94-213">You can optionally configure a schedule toostart and stop hello Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a><span data-ttu-id="3ce94-214">Добавление узлов Azure toohello кластера</span><span class="sxs-lookup"><span data-stu-id="3ce94-214">Add Azure nodes toohello cluster</span></span>
<span data-ttu-id="3ce94-215">Теперь можно используйте toohello кластера узлов Azure tooadd hello узла шаблона.</span><span class="sxs-lookup"><span data-stu-id="3ce94-215">Now use hello node template tooadd Azure nodes toohello cluster.</span></span> <span data-ttu-id="3ce94-216">Добавление кластера toohello узлы hello хранит сведения о конфигурации, чтобы можно было запускать (подготавливать) их в любое время в облачной службе hello.</span><span class="sxs-lookup"><span data-stu-id="3ce94-216">Adding hello nodes toohello cluster stores their configuration information so that you can start (provision) them at any time in hello cloud service.</span></span> <span data-ttu-id="3ce94-217">Подписки только возвращает взимается плата за узлов Azure после запущенных экземпляров hello в облачной службе hello.</span><span class="sxs-lookup"><span data-stu-id="3ce94-217">Your subscription only gets charged for Azure nodes after hello instances are running in hello cloud service.</span></span>

<span data-ttu-id="3ce94-218">Выполните эти шаги tooadd небольшой узлами.</span><span class="sxs-lookup"><span data-stu-id="3ce94-218">Follow these steps tooadd two Small nodes.</span></span>

1. <span data-ttu-id="3ce94-219">В диспетчере кластеров HPC выберите **Node Management** (Управление узлами) (в текущей версии пакета HPC **Управление ресурсами**) > **Добавить узел**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span></span>
   
    ![Добавить узел][add_node1]

2. <span data-ttu-id="3ce94-221">В hello мастер добавления узла в hello **Выбор метода развертывания** нажмите кнопку **узлов Windows Azure, добавить**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-221">In hello Add Node Wizard, on hello **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Добавление узла Azure][add_node1_1]

3. <span data-ttu-id="3ce94-223">На hello **укажите новые узлы** страницу, выберите hello шаблона узла Azure, созданной ранее (вызывается по умолчанию **шаблоном AzureNode по умолчанию**).</span><span class="sxs-lookup"><span data-stu-id="3ce94-223">On hello **Specify New Nodes** page, select hello Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="3ce94-224">Затем укажите **2** **мелких** узла и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![Указание узлов][add_node2]
   
4. <span data-ttu-id="3ce94-226">На hello **Здравствуйте, завершение работы мастера добавления узла** щелкните **Готово**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-226">On hello **Completing hello Add Node Wizard** page, click **Finish**.</span></span>
    
     <span data-ttu-id="3ce94-227">Два узла Azure с именем **AzureCN-0001** и **AzureCN-0002** появятся в диспетчере кластеров HPC.</span><span class="sxs-lookup"><span data-stu-id="3ce94-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="3ce94-228">Обе они находятся в hello **не развернуто** состояния.</span><span class="sxs-lookup"><span data-stu-id="3ce94-228">Both are in hello **Not-Deployed** state.</span></span>
   
    ![Добавленные узлы][add_node3]

## <a name="start-hello-azure-nodes"></a><span data-ttu-id="3ce94-230">Запуск hello узлов Azure</span><span class="sxs-lookup"><span data-stu-id="3ce94-230">Start hello Azure nodes</span></span>
<span data-ttu-id="3ce94-231">При необходимости ресурсы кластера hello toouse в Azure, используйте диспетчер кластеров HPC toostart (провизионирование) узлов Azure hello и перевести в оперативный режим.</span><span class="sxs-lookup"><span data-stu-id="3ce94-231">When you want toouse hello cluster resources in Azure, use HPC Cluster Manager toostart (provision) hello Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="3ce94-232">В диспетчере кластера HPC, нажмите кнопку **управления узлами** (называется **управление ресурсами** в текущей версии пакета HPC), и выберите hello узлов Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce94-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select hello Azure nodes.</span></span>

2. <span data-ttu-id="3ce94-233">Выберите **Запустить**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-233">Click **Start**, and then click **OK**.</span></span>
   
   ![Запуск узлов][add_node4]
   
    <span data-ttu-id="3ce94-235">узлы Hello переход toohello **Provisioning** состояния.</span><span class="sxs-lookup"><span data-stu-id="3ce94-235">hello nodes transition toohello **Provisioning** state.</span></span> <span data-ttu-id="3ce94-236">Представление hello подготовки hello tootrack журнала ход выполнения подготовки.</span><span class="sxs-lookup"><span data-stu-id="3ce94-236">View hello provisioning log tootrack hello provisioning progress.</span></span>
   
    ![Подготовка узлов][add_node6]

3. <span data-ttu-id="3ce94-238">Через несколько минут hello узлов Azure завершения подготовки и находятся в hello **Offline** состояния.</span><span class="sxs-lookup"><span data-stu-id="3ce94-238">After a few minutes, hello Azure nodes finish provisioning and are in hello **Offline** state.</span></span> <span data-ttu-id="3ce94-239">В этом состоянии hello экземпляров роли выполняются, но еще не может принимать задания кластера.</span><span class="sxs-lookup"><span data-stu-id="3ce94-239">In this state, hello role instances are running but cannot yet accept cluster jobs.</span></span>

4. <span data-ttu-id="3ce94-240">Запуск tooconfirm, hello экземпляров роли в hello портал Azure, щелкните **облачные службы (классические)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="3ce94-240">tooconfirm that hello role instances are running, in hello Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span></span>
   
   <span data-ttu-id="3ce94-241">Вы увидите два **HpcWorkerRole** экземпляров (узлов), выполняемых в службе hello.</span><span class="sxs-lookup"><span data-stu-id="3ce94-241">You should see two **HpcWorkerRole** instances (nodes) running in hello service.</span></span> <span data-ttu-id="3ce94-242">Пакет HPC также автоматически развертывает два **HpcProxy** экземпляров (размер среднего) toohandle взаимодействия между головным узлом hello и Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce94-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) toohandle communication between hello head node and Azure.</span></span>

   ![Выполняющиеся экземпляры][view_instances1]

5. <span data-ttu-id="3ce94-244">online toorun toobring hello Azure узлы кластера заданий, выберите hello узлов, щелкните правой кнопкой мыши и выберите команду **перевести в оперативный режим**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-244">toobring hello Azure nodes online toorun cluster jobs, select hello nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![Автономные узлы][add_node7]
   
    <span data-ttu-id="3ce94-246">Диспетчер кластеров HPC означает, что узлы hello в hello **Online** состояния.</span><span class="sxs-lookup"><span data-stu-id="3ce94-246">HPC Cluster Manager indicates that hello nodes are in hello **Online** state.</span></span>

## <a name="run-a-command-across-hello-cluster"></a><span data-ttu-id="3ce94-247">Выполнение команды в кластере hello</span><span class="sxs-lookup"><span data-stu-id="3ce94-247">Run a command across hello cluster</span></span>
<span data-ttu-id="3ce94-248">toocheck hello установки, используйте hello HPC Pack **clusrun** toorun команда команды или приложения на одном или нескольких узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="3ce94-248">toocheck hello installation, use hello HPC Pack **clusrun** command toorun a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="3ce94-249">В качестве простого примера используйте **clusrun** tooget hello IP-конфигурации hello узлов Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce94-249">As a simple example, use **clusrun** tooget hello IP configuration of hello Azure nodes.</span></span>

1. <span data-ttu-id="3ce94-250">На головном узле hello откройте командную строку с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="3ce94-250">On hello head node, open a command prompt as an administrator.</span></span>

2. <span data-ttu-id="3ce94-251">Введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="3ce94-251">Type hello following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`

3. <span data-ttu-id="3ce94-252">При появлении запроса введите пароль администратора кластера.</span><span class="sxs-lookup"><span data-stu-id="3ce94-252">If prompted, enter your cluster administrator password.</span></span> <span data-ttu-id="3ce94-253">Вы увидите примерно следующие toohello, выходных данных команды.</span><span class="sxs-lookup"><span data-stu-id="3ce94-253">You should see command output similar toohello following.</span></span>
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="3ce94-255">Выполнение тестового задания</span><span class="sxs-lookup"><span data-stu-id="3ce94-255">Run a test job</span></span>
<span data-ttu-id="3ce94-256">Теперь можно отправьте тестовое задание, запускаемую hello гибридный кластер.</span><span class="sxs-lookup"><span data-stu-id="3ce94-256">Now submit a test job that runs on hello hybrid cluster.</span></span> <span data-ttu-id="3ce94-257">Этот пример является простым заданием параметрического анализа (тип классических параллельных вычислений).</span><span class="sxs-lookup"><span data-stu-id="3ce94-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="3ce94-258">В этом примере выполняется подзадачи, добавить tooitself целое число со знаком, используя hello **set /a** команды.</span><span class="sxs-lookup"><span data-stu-id="3ce94-258">This example runs subtasks that add an integer tooitself by using hello **set /a** command.</span></span> <span data-ttu-id="3ce94-259">Все узлы hello кластера hello contribute подзадачи hello toofinishing для целых чисел от 1 too100.</span><span class="sxs-lookup"><span data-stu-id="3ce94-259">All hello nodes in hello cluster contribute toofinishing hello subtasks for integers from 1 too100.</span></span>

1. <span data-ttu-id="3ce94-260">В диспетчере кластеров HPC выберите **Управление заданиями** > **New Parametric Sweep Job** (Создать задание параметрического анализа).</span><span class="sxs-lookup"><span data-stu-id="3ce94-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span></span>
   
    ![Новое задание][test_job1]

2. <span data-ttu-id="3ce94-262">В hello **новое параметрической очистки задание** диалогового **командной строки**, тип `set /a *+*` (перезапись hello по умолчанию появится командной строки).</span><span class="sxs-lookup"><span data-stu-id="3ce94-262">In hello **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting hello default command line that appears).</span></span> <span data-ttu-id="3ce94-263">Оставьте значения по умолчанию для оставшихся параметров hello и нажмите кнопку **отправить** toosubmit hello задания.</span><span class="sxs-lookup"><span data-stu-id="3ce94-263">Leave default values for hello remaining settings, and then click **Submit** toosubmit hello job.</span></span>
   
    ![Параметрический анализ][param_sweep1]

3. <span data-ttu-id="3ce94-265">После завершения задания hello дважды щелкните hello **Мои задачи очистки** задания.</span><span class="sxs-lookup"><span data-stu-id="3ce94-265">When hello job is finished, double-click hello **My Sweep Task** job.</span></span>

4. <span data-ttu-id="3ce94-266">Нажмите кнопку **Просмотр задач**, а затем нажмите кнопку выходных данных вычисляется hello подзадаче tooview том же уровне.</span><span class="sxs-lookup"><span data-stu-id="3ce94-266">Click **View Tasks**, and then click a subtask tooview hello calculated output of that subtask.</span></span>
   
    ![Результаты выполнения задачи][view_job361]

5. <span data-ttu-id="3ce94-268">Нажмите кнопку toosee, какой из узлов для этой вложенной задачи выполняется вычисление hello **выделенных узлов**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-268">toosee which node performed hello calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="3ce94-269">(Кластер может показывать другое имя узла).</span><span class="sxs-lookup"><span data-stu-id="3ce94-269">(Your cluster might show a different node name.)</span></span>
   
    ![Результаты выполнения задачи][view_job362]

## <a name="stop-hello-azure-nodes"></a><span data-ttu-id="3ce94-271">Остановить hello узлов Azure</span><span class="sxs-lookup"><span data-stu-id="3ce94-271">Stop hello Azure nodes</span></span>
<span data-ttu-id="3ce94-272">После испытать hello кластера, остановите hello узлов Azure tooavoid ненужные расходы tooyour учетной записи.</span><span class="sxs-lookup"><span data-stu-id="3ce94-272">After you try out hello cluster, stop hello Azure nodes tooavoid unnecessary charges tooyour account.</span></span> <span data-ttu-id="3ce94-273">Этот шаг останавливает hello облачной службы и удаляет экземпляры роли Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3ce94-273">This step stops hello cloud service and removes hello Azure role instances.</span></span>

1. <span data-ttu-id="3ce94-274">В диспетчере кластеров HPC в разделе **Node Management** (Управление узлами) (в предыдущих версиях пакета HPC он называется **Управление ресурсами**) выберите оба узла Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce94-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="3ce94-275">Затем щелкните **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-275">Then, click **Stop**.</span></span>
   
    ![Остановка узлов][stop_node1]

2. <span data-ttu-id="3ce94-277">В hello **узлов Windows Azure остановить** диалоговое окно, нажмите кнопку **остановить**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-277">In hello **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span> 
   
3. <span data-ttu-id="3ce94-278">узлы Hello переход toohello **остановка** состояния.</span><span class="sxs-lookup"><span data-stu-id="3ce94-278">hello nodes transition toohello **Stopping** state.</span></span> <span data-ttu-id="3ce94-279">Через несколько минут диспетчера кластеров HPC показывает, что узлы hello **не развернуто**.</span><span class="sxs-lookup"><span data-stu-id="3ce94-279">After a few minutes, HPC Cluster Manager shows that hello nodes are **Not-Deployed**.</span></span>
   
    ![Неразвернутые узлы][stop_node4]

4. <span data-ttu-id="3ce94-281">Здравствуйте, tooconfirm, экземпляры роли hello больше не выполняется в Azure, в Azure, щелкните **облачные службы (классические)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="3ce94-281">tooconfirm that hello role instances are no longer running in Azure, in hello Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span></span> <span data-ttu-id="3ce94-282">Экземпляры не будут развернуты в рабочей среде hello.</span><span class="sxs-lookup"><span data-stu-id="3ce94-282">No instances are deployed in hello production environment.</span></span> 
   
    <span data-ttu-id="3ce94-283">На этом учебник hello.</span><span class="sxs-lookup"><span data-stu-id="3ce94-283">This completes hello tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ce94-284">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3ce94-284">Next steps</span></span>
* <span data-ttu-id="3ce94-285">Просмотр документации hello для [HPC Pack](https://technet.microsoft.com/library/cc514029).</span><span class="sxs-lookup"><span data-stu-id="3ce94-285">Explore hello documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="3ce94-286">tooset копирование гибридного развертывания кластера HPC Pack в масштабе выше, в разделе [прорыв tooAzure экземпляров рабочей роли с помощью пакета Microsoft HPC](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="3ce94-286">tooset up a hybrid HPC Pack cluster deployment at greater scale, see [Burst tooAzure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="3ce94-287">Для других способов toocreate кластере HPC Pack в Azure, включая использование шаблонов диспетчера ресурсов Azure, см. в [параметры кластера HPC с помощью пакета Microsoft HPC в Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3ce94-287">For other ways toocreate an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
