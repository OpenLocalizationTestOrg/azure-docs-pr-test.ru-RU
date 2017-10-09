---
title: " Управление сервером обработки, запущенным в Azure (классическая модель) | Документация Майкрософт"
description: "В этой статье описывается как tooset копирование и восстановление после сбоя процесса Server(Classic) в Azure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="7f47d-103">Управление сервером обработки, запущенным в Azure (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="7f47d-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f47d-104">Классическая модель Azure</span><span class="sxs-lookup"><span data-stu-id="7f47d-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="7f47d-105">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="7f47d-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="7f47d-106">При отработке отказа toodeploy сервера обработки в Azure рекомендуется при наличии высокой задержки между hello виртуальной сети Azure и локальной сетью.</span><span class="sxs-lookup"><span data-stu-id="7f47d-106">During failback, it is recommended toodeploy Process Server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="7f47d-107">В этой статье описывается, как установить, настроить и управлять серверами процесса hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="7f47d-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="7f47d-108">Эта статья является toobe, используемый при использовании классической модели развертывания hello hello виртуальных машин во время отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="7f47d-108">This article is toobe used if you used Classic as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="7f47d-109">При использовании диспетчера ресурсов, как hello hello развертывания модели повторите шаги в [как tooset о & Настройка восстановления размещения процесса сервера (диспетчера ресурсов)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="7f47d-109">If you used Resource Manager as hello deployment model follow hello steps in [How tooset up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f47d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7f47d-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="7f47d-111">Развертывание сервера обработки в Azure</span><span class="sxs-lookup"><span data-stu-id="7f47d-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="7f47d-112">В Azure Marketplace, создайте виртуальную машину, используя hello **сервера Microsoft Azure сайта восстановления процесса V2**</span><span class="sxs-lookup"><span data-stu-id="7f47d-112">In Azure Marketplace, create a virtual machine using hello **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="7f47d-113">![](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)Marketplace_image_1</span><span class="sxs-lookup"><span data-stu-id="7f47d-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="7f47d-114">Убедитесь, что вы выбрали hello модель развертывания как **классический**</span><span class="sxs-lookup"><span data-stu-id="7f47d-114">Ensure that you select hello deployment model as **Classic**</span></span> </br><span data-ttu-id="7f47d-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="7f47d-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="7f47d-116">В мастере виртуальной машины создать hello > Основные параметры, убедитесь, вы выбрали hello подписке и расположении toowhere, отработку отказа виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="7f47d-116">In hello Create virtual machine wizard > Basic Settings, ensure you select hello Subscription and Location toowhere you failed over hello virtual machines.</span></span></br><span data-ttu-id="7f47d-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="7f47d-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="7f47d-118">Убедитесь, что на виртуальной машине hello подключен подключен toohello виртуальной сети Azure toowhich hello отработку отказа виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7f47d-118">Ensure that hello virtual machine is connected toohello Azure Virtual Network toowhich hello failed over virtual machine is connected.</span></span></br><span data-ttu-id="7f47d-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="7f47d-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="7f47d-120">После подготовки виртуальной машины hello процесса сервера, требуется toolog в и зарегистрируйте его в hello сервера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7f47d-120">Once hello Process Server virtual machine is provisioned, you need toolog in and register it with hello Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="7f47d-121">возможности toouse toobe сервер обработки для восстановления размещения, должны tooregister его с сервера конфигурации локальной hello.</span><span class="sxs-lookup"><span data-stu-id="7f47d-121">toobe able toouse this Process Server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="7f47d-122">Регистрация tooa процесса сервера (под управлением Azure) hello конфигурации сервер (локальный)</span><span class="sxs-lookup"><span data-stu-id="7f47d-122">Registering hello Process Server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="7f47d-123">Обновление версии toolatest hello сервер обработки.</span><span class="sxs-lookup"><span data-stu-id="7f47d-123">Upgrading hello Process Server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="7f47d-124">Отмена регистрации hello процесса сервера (под управлением Azure) от конфигурации (выполняется локально)</span><span class="sxs-lookup"><span data-stu-id="7f47d-124">Unregistering hello Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
