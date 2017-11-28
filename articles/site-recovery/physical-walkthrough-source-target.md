---
title: "aaaSet hello исходного и целевого объекта для физического сервера tooAzure репликации с помощью Azure Site Recovery | Документы Microsoft"
description: "Перечислены tooset действия hello исходных и целевых параметров репликации хранилища tooAzure физических серверов со службой Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a><span data-ttu-id="0e5a6-103">Шаг 7: Настройка hello исходной и целевой для tooAzure репликации физического сервера</span><span class="sxs-lookup"><span data-stu-id="0e5a6-103">Step 7: Set up hello source and target for physical server replication tooAzure</span></span>

<span data-ttu-id="0e5a6-104">В этой статье описывается, как tooconfigure источника и целевых параметров при репликации локально tooAzure физических серверов, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-104">This article describes how tooconfigure source and target settings when replicating on-premises physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="0e5a6-105">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0e5a6-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="0e5a6-106">Настройка среды источника hello</span><span class="sxs-lookup"><span data-stu-id="0e5a6-106">Set up hello source environment</span></span>

<span data-ttu-id="0e5a6-107">Настройка сервера конфигурации hello, зарегистрируйте его в хранилище hello и обнаружение компьютеров.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-107">Set up hello configuration server, register it in hello vault, and discover machines.</span></span>

1. <span data-ttu-id="0e5a6-108">Щелкните **Site Recovery** > **Шаг 1. Подготовка инфраструктуры** > **Источник**.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="0e5a6-109">Если у вас нет сервера конфигурации, щелкните **+Configuration server** (+ Сервер конфигурации).</span><span class="sxs-lookup"><span data-stu-id="0e5a6-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="0e5a6-110">В колонке **Добавление сервера** в поле **Тип сервера** должно быть указано **Сервер конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="0e5a6-111">Загрузите файл установки hello установка единой Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="0e5a6-112">Загрузите ключ регистрации в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-112">Download hello vault registration key.</span></span> <span data-ttu-id="0e5a6-113">Он потребуется при запуске единой установки.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="0e5a6-114">Hello ключ действителен в течение пяти дней после его создания.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-114">hello key is valid for five days after you generate it.</span></span>

   ![Настройка источника](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="0e5a6-116">Зарегистрируйте сервер конфигурации hello в хранилище hello</span><span class="sxs-lookup"><span data-stu-id="0e5a6-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="0e5a6-117">Следующие hello, прежде чем начать, а затем выполните tooinstall hello конфигурации сервера, сервера обработки hello и главный целевой сервер hello единой программы установки.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span> <span data-ttu-id="0e5a6-118">Hello видео Настройка компонентов hello tooAzure репликации виртуальной Машины VMware.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-118">hello video describes setting up hello components for VMware VM tooAzure replication.</span></span> <span data-ttu-id="0e5a6-119">Однако hello одного процесса является допустимым для репликации tooAzure физического сервера.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-119">However, hello same process is valid for physical server tooAzure replication.</span></span>

- <span data-ttu-id="0e5a6-120">На сервере конфигурации hello виртуальной Машины, убедитесь, что системные часы, hello синхронизируется с [сервер времени](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="0e5a6-120">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="0e5a6-121">Значения времени должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-121">It should match.</span></span> <span data-ttu-id="0e5a6-122">Если системные часы отстают или спешат в пределах 15 минут, установка может завершиться ошибкой.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="0e5a6-123">Запустите программу установки локального администратора на сервере конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-123">Run setup as a Local Administrator on hello configuration server machine.</span></span>
- <span data-ttu-id="0e5a6-124">Убедитесь в том, что протоколы TLS 1.0 включен в hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-124">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="0e5a6-125">также можно установить сервер конфигурации Hello [из командной строки hello](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="0e5a6-125">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-hello-target-environment"></a><span data-ttu-id="0e5a6-126">Настройка целевой среды hello</span><span class="sxs-lookup"><span data-stu-id="0e5a6-126">Set up hello target environment</span></span>

<span data-ttu-id="0e5a6-127">Перед настройкой hello целевой среде, убедитесь, что у вас есть учетная запись хранения Azure и настройка виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-127">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="0e5a6-128">Нажмите кнопку **подготовки инфраструктуры** > **целевой**, и выберите hello требуется toouse подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-128">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="0e5a6-129">Укажите, какая целевая модель развертывания используется: классическая или Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="0e5a6-130">Site Recovery проверяет наличие одной или нескольких совместимых учетных записей хранения и сетей Azure.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Цель](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="0e5a6-132">Если вы еще не создали учетную запись хранения или сети, нажмите кнопку **+ учетная запись хранения** или **+ сети**, toocreate диспетчера ресурсов учетной записи или сети встроенной.</span><span class="sxs-lookup"><span data-stu-id="0e5a6-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e5a6-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0e5a6-133">Next steps</span></span>

<span data-ttu-id="0e5a6-134">Go слишком[Step 8: настроить политику репликации](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="0e5a6-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
