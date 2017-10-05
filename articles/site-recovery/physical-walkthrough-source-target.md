---
title: "Настройка исходной и целевой среды для репликации физического сервера в Azure с помощью Azure Site Recovery | Документация Майкрософт"
description: "В этой статье кратко описаны шаги для настройки параметров исходной и целевой среды при репликации физических серверов в службу хранилища Azure с помощью службы Azure Site Recovery."
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
ms.openlocfilehash: e89bbf5a2c1d71852e49da43d3106a05ebfc28a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-the-source-and-target-for-physical-server-replication-to-azure"></a><span data-ttu-id="f3511-103">Шаг 7. Настройка исходной и целевой среды для репликации физического сервера в Azure</span><span class="sxs-lookup"><span data-stu-id="f3511-103">Step 7: Set up the source and target for physical server replication to Azure</span></span>

<span data-ttu-id="f3511-104">В этой статье описано, как настроить параметры исходной и целевой среды при репликации локальных физических серверов в Azure с помощью службы [Azure Site Recovery](site-recovery-overview.md) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f3511-104">This article describes how to configure source and target settings when replicating on-premises physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="f3511-105">Комментарии или вопросы можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f3511-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="f3511-106">Настройка исходной среды</span><span class="sxs-lookup"><span data-stu-id="f3511-106">Set up the source environment</span></span>

<span data-ttu-id="f3511-107">Настройте сервер конфигурации, зарегистрируйте его в хранилище и найдите виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="f3511-107">Set up the configuration server, register it in the vault, and discover machines.</span></span>

1. <span data-ttu-id="f3511-108">Щелкните **Site Recovery** > **Шаг 1. Подготовка инфраструктуры** > **Источник**.</span><span class="sxs-lookup"><span data-stu-id="f3511-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="f3511-109">Если у вас нет сервера конфигурации, щелкните **+Configuration server** (+ Сервер конфигурации).</span><span class="sxs-lookup"><span data-stu-id="f3511-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="f3511-110">В колонке **Добавление сервера** в поле **Тип сервера** должно быть указано **Сервер конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="f3511-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="f3511-111">Скачайте файл единой установки Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f3511-111">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="f3511-112">Скачайте ключ регистрации хранилища.</span><span class="sxs-lookup"><span data-stu-id="f3511-112">Download the vault registration key.</span></span> <span data-ttu-id="f3511-113">Он потребуется при запуске единой установки.</span><span class="sxs-lookup"><span data-stu-id="f3511-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="f3511-114">Ключ действителен в течение пяти дней после создания.</span><span class="sxs-lookup"><span data-stu-id="f3511-114">The key is valid for five days after you generate it.</span></span>

   ![Настройка источника](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-the-configuration-server-in-the-vault"></a><span data-ttu-id="f3511-116">Регистрация сервера конфигурации в хранилище</span><span class="sxs-lookup"><span data-stu-id="f3511-116">Register the configuration server in the vault</span></span>

<span data-ttu-id="f3511-117">Прежде чем начать, выполните приведенные ниже действия, после чего запустите программу единой установки, чтобы установить сервер конфигурации, сервер обработки и главный целевой сервер.</span><span class="sxs-lookup"><span data-stu-id="f3511-117">Do the following before you start, then run Unified Setup to install the configuration server, the process server, and the master target server.</span></span> <span data-ttu-id="f3511-118">Просмотрите видео, в котором описано настройку компонентов для репликации виртуальных машин VMware в Azure.</span><span class="sxs-lookup"><span data-stu-id="f3511-118">The video describes setting up the components for VMware VM to Azure replication.</span></span> <span data-ttu-id="f3511-119">Но этот процесс можно также применить при репликации физического сервера в Azure.</span><span class="sxs-lookup"><span data-stu-id="f3511-119">However, the same process is valid for physical server to Azure replication.</span></span>

- <span data-ttu-id="f3511-120">Убедитесь, что на виртуальной машине сервера конфигурации системные часы синхронизированы с [сервером времени](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="f3511-120">On the configuration server VM, make sure that the system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="f3511-121">Значения времени должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="f3511-121">It should match.</span></span> <span data-ttu-id="f3511-122">Если системные часы отстают или спешат в пределах 15 минут, установка может завершиться ошибкой.</span><span class="sxs-lookup"><span data-stu-id="f3511-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="f3511-123">На компьютере сервера конфигурации запустите программу установки от имени локального администратора.</span><span class="sxs-lookup"><span data-stu-id="f3511-123">Run setup as a Local Administrator on the configuration server machine.</span></span>
- <span data-ttu-id="f3511-124">Включите на компьютере протокол TLS 1.0.</span><span class="sxs-lookup"><span data-stu-id="f3511-124">Make sure TLS 1.0 is enabled on the VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="f3511-125">Сервер конфигурации можно также установить [с помощью командной строки](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="f3511-125">The configuration server can also be installed [from the command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-the-target-environment"></a><span data-ttu-id="f3511-126">Настройка целевой среды</span><span class="sxs-lookup"><span data-stu-id="f3511-126">Set up the target environment</span></span>

<span data-ttu-id="f3511-127">Перед настройкой целевой среды убедитесь, что учетная запись хранения Azure и виртуальная сеть настроены.</span><span class="sxs-lookup"><span data-stu-id="f3511-127">Before you set up the target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="f3511-128">Щелкните **Подготовка инфраструктуры** > **Цель** и выберите требуемую подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="f3511-128">Click **Prepare infrastructure** > **Target**, and select the Azure subscription you want to use.</span></span>
2. <span data-ttu-id="f3511-129">Укажите, какая целевая модель развертывания используется: классическая или Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f3511-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="f3511-130">Site Recovery проверяет наличие одной или нескольких совместимых учетных записей хранения и сетей Azure.</span><span class="sxs-lookup"><span data-stu-id="f3511-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Цель](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="f3511-132">Если вы еще не создали учетную запись хранения или сеть, щелкните **+Учетная запись хранения** или **+Сеть**, чтобы создать учетную запись Resource Manager или сеть.</span><span class="sxs-lookup"><span data-stu-id="f3511-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, to create a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3511-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f3511-133">Next steps</span></span>

<span data-ttu-id="f3511-134">Перейдите к разделу [Шаг 8. Настройка политики репликации для репликации физического сервера в Azure](physical-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="f3511-134">Go to [Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
