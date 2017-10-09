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
# <a name="manage-a-process-server-running-in-azure-classic"></a>Управление сервером обработки, запущенным в Azure (классическая модель)
> [!div class="op_single_selector"]
> * [Классическая модель Azure](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [Диспетчер ресурсов](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

При отработке отказа toodeploy сервера обработки в Azure рекомендуется при наличии высокой задержки между hello виртуальной сети Azure и локальной сетью. В этой статье описывается, как установить, настроить и управлять серверами процесса hello в Azure.

> [!NOTE]
> Эта статья является toobe, используемый при использовании классической модели развертывания hello hello виртуальных машин во время отработки отказа. При использовании диспетчера ресурсов, как hello hello развертывания модели повторите шаги в [как tooset о & Настройка восстановления размещения процесса сервера (диспетчера ресурсов)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

## <a name="prerequisites"></a>Предварительные требования

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Развертывание сервера обработки в Azure

1. В Azure Marketplace, создайте виртуальную машину, используя hello **сервера Microsoft Azure сайта восстановления процесса V2** </br>
    ![](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)Marketplace_image_1
2. Убедитесь, что вы выбрали hello модель развертывания как **классический** </br>
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)
3. В мастере виртуальной машины создать hello > Основные параметры, убедитесь, вы выбрали hello подписке и расположении toowhere, отработку отказа виртуальных машин hello.</br>
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)
4. Убедитесь, что на виртуальной машине hello подключен подключен toohello виртуальной сети Azure toowhich hello отработку отказа виртуальной машины.</br>
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)
5. После подготовки виртуальной машины hello процесса сервера, требуется toolog в и зарегистрируйте его в hello сервера конфигурации.

> [!NOTE]
> возможности toouse toobe сервер обработки для восстановления размещения, должны tooregister его с сервера конфигурации локальной hello.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>Регистрация tooa процесса сервера (под управлением Azure) hello конфигурации сервер (локальный)

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>Обновление версии toolatest hello сервер обработки.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>Отмена регистрации hello процесса сервера (под управлением Azure) от конфигурации (выполняется локально)

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
