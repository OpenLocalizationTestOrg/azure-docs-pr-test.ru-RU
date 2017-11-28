---
title: "Настройка исходной и целевой среды для репликации Hyper-V в Azure (без System Center VMM) с помощью Azure Site Recovery | Документация Майкрософт"
description: "В этой статье кратко описаны шаги для настройки параметров исходной и целевой среды при репликации виртуальных машин Hyper-V в службу хранилища Azure с помощью Azure Site Recovery."
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
ms.openlocfilehash: b38eb3a011d46f2239891ea1d1bcac2a4059a866
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-the-source-and-target-for-hyper-v-replication-to-azure"></a><span data-ttu-id="53545-103">Шаг 8. Настройка исходной и целевой среды для репликации из Hyper-V в Azure</span><span class="sxs-lookup"><span data-stu-id="53545-103">Step 8: Set up the source and target for Hyper-V replication to Azure</span></span>

<span data-ttu-id="53545-104">В этой статье описано, как настроить параметры исходной и целевой среды при репликации локальных виртуальных машин Hyper-V (без System Center VMM) в Azure с помощью службы [Azure Site Recovery](site-recovery-overview.md) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="53545-104">This article describes how to configure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="53545-105">Комментарии или вопросы можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="53545-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="53545-106">Настройка исходной среды</span><span class="sxs-lookup"><span data-stu-id="53545-106">Set up the source environment</span></span>

<span data-ttu-id="53545-107">Настройте узел Hyper-V, установите поставщика Azure Site Recovery и агента служб восстановления Azure на узлах Hyper-V, затем зарегистрируйте сайт в хранилище.</span><span class="sxs-lookup"><span data-stu-id="53545-107">Set up the Hyper-V site, install the Azure Site Recovery Provider and the Azure Recovery Services agent on Hyper-V hosts, and register the site in the vault.</span></span>

1. <span data-ttu-id="53545-108">В разделе **Подготовка инфраструктуры** щелкните **Источник**.</span><span class="sxs-lookup"><span data-stu-id="53545-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="53545-109">Чтобы добавить новый узел Hyper-V в качестве контейнера для узлов или кластеров Hyper-V, щелкните **+Hyper-V Site**(+ Сайт Hyper-V).</span><span class="sxs-lookup"><span data-stu-id="53545-109">To add a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![Настройка источника](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="53545-111">В колонке **Создание сайта Hyper-V** укажите имя для сайта.</span><span class="sxs-lookup"><span data-stu-id="53545-111">In **Create Hyper-V site**, specify a name for the site.</span></span> <span data-ttu-id="53545-112">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="53545-112">Then click **OK**.</span></span> <span data-ttu-id="53545-113">Теперь выберите созданный сайт и щелкните действие **Добавить сервер Hyper-V**, чтобы добавить сервер на сайт.</span><span class="sxs-lookup"><span data-stu-id="53545-113">Now, select the site you created, and click **+Hyper-V Server** to add a server to the site.</span></span>

    ![Настройка источника](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="53545-115">Убедитесь, что **сервер Hyper-V** отображается в разделе **Добавить сервер** > **Тип сервера**.</span><span class="sxs-lookup"><span data-stu-id="53545-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="53545-116">Убедитесь, что сервер Hyper-V Server, который вы хотите добавить, соответствует [предварительным требованиям](#on-premises-prerequisites) и имеет доступ к указанным URL-адресам.</span><span class="sxs-lookup"><span data-stu-id="53545-116">Make sure that the Hyper-V server you want to add complies with the [prerequisites](#on-premises-prerequisites), and is able to access the specified URLs.</span></span>
    - <span data-ttu-id="53545-117">Скачайте файл установки поставщика Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="53545-117">Download the Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="53545-118">Запустите этот файл, чтобы установить поставщик и агент служб восстановления на каждый узел Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="53545-118">You run this file to install the Provider and the Recovery Services agent on each Hyper-V host.</span></span>

    ![Настройка источника](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-the-provider-and-agent"></a><span data-ttu-id="53545-120">Установка поставщика и агента</span><span class="sxs-lookup"><span data-stu-id="53545-120">Install the Provider and agent</span></span>

1. <span data-ttu-id="53545-121">Запустите файл установки поставщика на каждом узле, добавленном в узел Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="53545-121">Run the Provider setup file on each host you added to the Hyper-V site.</span></span> <span data-ttu-id="53545-122">Если установка выполняется в кластер Hyper-V, программу установки необходимо запустить на каждом узле кластера.</span><span class="sxs-lookup"><span data-stu-id="53545-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="53545-123">Установка и регистрация всех узлов кластера Hyper-V гарантирует, что виртуальные машины будут защищены даже при переносе между узлами.</span><span class="sxs-lookup"><span data-stu-id="53545-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="53545-124">Обновления можно включить на странице **Центр обновления Майкрософт**. Это позволит устанавливать обновления поставщика в соответствии с политикой Центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="53545-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="53545-125">На странице **Установка** примите или измените расположение установки поставщика по умолчанию и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="53545-125">In **Installation**, accept or modify the default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="53545-126">На странице **Параметры хранилища** нажмите кнопку **Обзор**, чтобы выбрать скачанный файл ключа хранилища.</span><span class="sxs-lookup"><span data-stu-id="53545-126">In **Vault Settings**, click **Browse** to select the vault key file that you downloaded.</span></span> <span data-ttu-id="53545-127">Укажите подписку Azure Site Recovery, имя хранилища и узла Hyper-V, к которому относится сервер Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="53545-127">Specify the Azure Site Recovery subscription, the vault name, and the Hyper-V site to which the Hyper-V server belongs.</span></span>

    ![Регистрация сервера](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="53545-129">В окне **Параметры Интернета** укажите параметры для подключения поставщика, который будет выполняться на узлах Hyper-V, к Azure Site Recovery через Интернет.</span><span class="sxs-lookup"><span data-stu-id="53545-129">In **Proxy Settings**, specify how the Provider running on Hyper-V hosts connects to Azure Site Recovery over the internet.</span></span>

    * <span data-ttu-id="53545-130">Чтобы поставщик подключался напрямую, установите переключатель **Подключиться к Azure Site Recovery напрямую без прокси-сервера**.</span><span class="sxs-lookup"><span data-stu-id="53545-130">If you want the Provider to connect directly select **Connect directly to Azure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="53545-131">Если для имеющегося прокси-сервера требуется проверка подлинности или для подключения к провайдеру нужно использовать пользовательский прокси-сервер, выберите **Подключиться к Azure Site Recovery с использованием прокси-сервера**.</span><span class="sxs-lookup"><span data-stu-id="53545-131">If your existing proxy requires authentication, or you want to use a custom proxy for the Provider connection, select **Connect to Azure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="53545-132">При использовании прокси-сервера:</span><span class="sxs-lookup"><span data-stu-id="53545-132">If you use a proxy:</span></span>
        - <span data-ttu-id="53545-133">укажите адрес, порт и учетные данные;</span><span class="sxs-lookup"><span data-stu-id="53545-133">Specify the address, port, and credentials</span></span>
        - <span data-ttu-id="53545-134">убедитесь, что он не блокирует URL-адреса, описанные в [предварительных требованиях](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="53545-134">Make sure the URLs described in the [prerequisites](#prerequisites) are allowed through the proxy.</span></span>

    ![Интернет](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="53545-136">После завершения установки нажмите кнопку **Зарегистрировать**, чтобы зарегистрировать сервер в хранилище.</span><span class="sxs-lookup"><span data-stu-id="53545-136">After installation finishes, click **Register** to register the server in the vault.</span></span>

    ![Расположение установки](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="53545-138">Когда регистрация завершится, Azure Site Recovery извлечет метаданные с сервера Hyper-V, а сам сервер отобразится в колонке **Инфраструктура Site Recovery**  > **Узлы Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="53545-138">After registration finishes, metadata from the Hyper-V server is retrieved by Azure Site Recovery, and the server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="53545-139">Настройка целевой среды</span><span class="sxs-lookup"><span data-stu-id="53545-139">Set up the target environment</span></span>

<span data-ttu-id="53545-140">Укажите учетную запись хранения Azure для репликации и сеть Azure, к которой будут подключаться виртуальные машины Azure после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="53545-140">Specify the Azure storage account for replication, and the Azure network to which Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="53545-141">Выберите **Подготовка инфраструктуры** > **Цель**.</span><span class="sxs-lookup"><span data-stu-id="53545-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="53545-142">Выберите подписку и группу ресурсов, в которых вы хотите создавать виртуальные машины Azure после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="53545-142">Select the subscription and the resource group in which you want to create the Azure VMs after failover.</span></span> <span data-ttu-id="53545-143">Выберите модель развертывания, которая будет использоваться в Azure (классическая или Resource Manager) для этих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="53545-143">Choose the deployment model that you want to use in Azure (classic or resource management) for the VMs.</span></span>

3. <span data-ttu-id="53545-144">Site Recovery проверяет наличие одной или нескольких совместимых учетных записей хранения и сетей Azure.</span><span class="sxs-lookup"><span data-stu-id="53545-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="53545-145">Если у вас нет учетной записи хранения, нажмите кнопку **+Хранилище**, чтобы прямо сейчас создать учетную запись на основе модели Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="53545-145">If you don't have a storage account, click **+Storage** to create a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="53545-146">Если у вас нет учетной сети Azure, нажмите кнопку **+Сеть**, чтобы прямо сейчас создать сеть на основе модели Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="53545-146">If you don't have a Azure network, click **+Network** to create a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="53545-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="53545-147">Next steps</span></span>

<span data-ttu-id="53545-148">Перейдите к разделу [Шаг 9. Настройка политики репликации для репликации физического сервера в Azure](hyper-v-site-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="53545-148">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
